## Verilog中的基本电路单元：

### 思维导图：

![](https://nickaljy-pictures.oss-cn-hangzhou.aliyuncs.com/img/基本电路单元1：.jpg)

### 1.三态总线：

![](https://nickaljy-pictures.oss-cn-hangzhou.aliyuncs.com/img/未命名文件 (1).jpg)

- 中间的三角不表示一个反相器，这个符号是三态门的标识符号。

- En是使能端口：

  - 当En的值为1的时候，Out的输出值为In的输入值。
  - 当En的值为0的时候，Out的输出值为``高阻态z``。

- 代码实现：

  - ```verilog
    module Top(In , En , Out)
        input In , En;
        output Out;
        
        assign:Out = En ? In : 1'bz;
    endmodule
    ```

    - 上述代码实现了一个三态总线(三态门)。
    - 注意，我们默认规定不在除了顶层模块以外的其他任何模块使用高阻态z，因此该模块我们命名为Top,表示这是一个顶层模块。

#### 2.半加器：

- 半加器是对两个1bit数据进行相加操作，结果为1位，进位为1位。

![](https://nickaljy-pictures.oss-cn-hangzhou.aliyuncs.com/img/未命名文件 (2).jpg)

- 四种情况：

  - 当in_1 = 0 , in_2 = 0时，out = 0 , carry = 0;
  - 当in_1 = 0 , in_2 = 1时，out = 1 , carry = 0;
  - 当in_1 = 1 , in_2 = 0时，out = 1 , carry = 0;
  - 当in_1 = 1 , in_2 = 1时，out = 0 , carry = 1;

- 代码实现：

  - ```verilog
    module half_adder(in_1 , in_2 , out , carry)
        input in_1 , in_2;
        output out , carry;
        
        assign out = in_1 ^ in_2;
        assign carry = in_1 & in_2;
        //根据上面的真值表，当in_1 and in_2不同的时候，out为1，因此对out执行异或操作。
        //当in_1 and in_2全部为1的时候，carry为1，因此对carry执行相与操作。
    endmodule
    ```

#### 3.全加器：

- 全加器是两个1bit的数据以及一个1bit的进位进行相加操作，结果为1位，进位为1位。

![](https://nickaljy-pictures.oss-cn-hangzhou.aliyuncs.com/img/未命名文件 (3).jpg)

- 八种情况：

  - 当in_1 = 0，in_2 = 0，carry_1 = 0时，out = 0，carry_2 = 0；
  - 当in_1 = 0，in_2 = 0，carry_1 = 1时，out = 1，carry_2 = 0；
  - 当in_1 = 0，in_2 = 1，carry_1 = 0时，out = 1，carry_2 = 0；
  - 当in_1 = 0，in_2 = 1，carry_1 = 1时，out = 0，carry_2 = 1；
  - 当in_1 = 1，in_2 = 0，carry_1 = 0时，out = 1，carry_2 = 0；
  - 当in_1 = 1，in_2 = 0，carry_1 = 1时，out = 0，carry_2 = 1；
  - 当in_1 = 1，in_2 = 1，carry_1 = 0时，out = 0，carry_2 = 1；
  - 当in_1 = 1，in_2 = 1，carry_1 = 1时，out = 1，carry_2 = 1；

- 代码实现：

  - ```verilog
    module full_adder(in_1 , in_2 , carry_1 , out , carry_2)
        input in_1 , in_2 , carry_1;
        output out , carry_2;
        
        assign out = (~in_1) & (~in_2) & carry_1 | (~in_1) & in_2 & (~carry_1) | in_1 & (~in_2) & (~carry) | in_1 & in_2 & carry_1;
        assign carry_2 = in_1 & in_2 | in_1 & carry_1 | in_2 & carry_1;
    endmodule
    ```

  - 上述代码是根据真值表以及卡诺图化简而来的逻辑函数表达式。

    - 我们可以发现，如果去这么设计电路的话，就不是RTL级的电路描述了，而是门级的电路描述，因此我们要避免这种设计方式。

- 对于全加器，我们有更简单的设计方式，即用两个半加器组成一个全加器：

![](https://nickaljy-pictures.oss-cn-hangzhou.aliyuncs.com/img/未命名文件 (4).jpg)

- 原理图分析：

  - 对于in_1 and in_2 and carry_1这三个输入值，我们是分别相加，首先将in_1 and in_2相加，结果保存在temp_1中，进位保存在temp_2中。
  - 之后将temp_1 and carry_1相加，结果直接就是out的值。
  - 这里要注意，carry_1的值可以是任意；而temp_1和temp_2的值相关联。
    - 如果temp_1 = 0，则temp_2可以是1也可以是0，而此时temp_3的值一定是0，此时temp_2的值就是整个全加器的进位。
    - 如果temp_1 = 1，则temp_2一定为0，此时temp_3的值可以为1也可以为0，并且此时temp_3的值就是整个全加器的进位。
  - 因此，我们选择把两个半加器的进位``相或``，得到的就是全加器的进位。

- 代码实现：

  - ```verilog
    module full_adder(in_1 , in_2 , carry_1 , out , carry_2)
        input in_1 , in_2 , carry_1;
        output out , carry_2;
        
        wire temp_1 , temp_2 , temp_3;
        
        half_adder hadder_1 (.in_1(in_1),.in_2(in_2),.out(temp_1),.carry(temp_2));
        half_adder hadder_2 (.in_1(carry_1),.in_2(temp_1),.out(out),.carry(temp_3));
        //实例化两个半加器模块。
        assign:carry_2 = temp_2 | temp_3;
    endmodule
    ```

#### 4.二选一选择器：

- 我们用Verilog对选择器进行建模的时候，大多数情况会考虑``if   else``语句，或者``case``语句。
- 注意在使用``if   else``的时候，一定要把``else``搭配上，否则容易出现锁存器；同理，在使用``case``的时候，一定要在最后搭配上``default``。
- 原理图：
  - ![](https://nickaljy-pictures.oss-cn-hangzhou.aliyuncs.com/img/未命名文件 (11).jpg)

- 上图所示的二选一选择器，工作原理是：

  - in_1 and in_2都是1bit的数据，sel也是1bit的数据。(当然，也可以不是1bit的数据)
  - 当sel = 0时，out的值是in_1的值；
  - 当sel = 1时，out的值是in_2的值。

- 代码实现：

  - ```verilog
    module Two_one_Plexer(in_1 , in_2 , sel , out)
        input in_1 , in_2 , sel;
        output out;
        
        assign: out = sel ? in_2 : in_1;
    endmodule
    ```

  - 上面是二选一选择器**最简单**的代码表示形式，这里使用的是一个``assign语句`` + ``?表达式``。

  - ```verilog
    module Two_one_Plexer(in_1 , in_2 , sel , out)
        input in_1 , in_2 , sel;
        output out;
        
        reg out;
        
        always @(in_1 , in_2 , sel)
        begin
            if (!sel)
                out = in_1;
            else
                out = in_2;
        end
    endmodule
    ```

  - 这是使用``if else``语句实现的代码，由于``if  else``语句要用在always语句中，因此我们要把out定义成reg类型。

#### 5.四选一选择器：

- 四选一选择器指的是：在四个数据中选择一个数据进行输出。(注意，被选择的数据不一定是一位)

- 原理图：
  - ![](https://nickaljy-pictures.oss-cn-hangzhou.aliyuncs.com/img/四选一选择器.jpg)

- 由于有四个选择位，因此选择信号需要两个：

  - 当sel_1 = 0 , sel_2 = 0时，out = in_1；
  - 当sel_1 = 0 , sel_2 = 1时，out = in_2；
  - 当sel_1 = 1 , sel_2 = 0时，out = in_3；
  - 当sel_1 = 1 , sel_2 = 1时，out = in_4；

- 代码实现:

  - ```verilog
    module Four_one_Plexer(in_1 , in_2 , in_3 , in_4 , sel_1 , sel_2 , out)
        input in_1 , in_2 , in_3 , in_4 , sel_1 , sel_2;
        output out;
        
        reg out;
        
        always @(in_1 , in_2 , in_3 , in_4 , sel_1 , sel_2)
        begin
            if (sel_1 == 1'b0 && sel_2 == 1'b0)
                out = in_1;
            else if (sel_1 == 1'b0 && sel_2 == 1'b1)
                out = in_2;
            else if (sel_1 == 1'b1 && sel_2 == 1'b0)
                out = in_3;
            else
                out = in_4;
        end
    endmodule
    ```

  - 上述代码是用``if else``实现的，注意不要产生锁存器。

  - ```verilog
    module Four_one_Plexer(in_1 , in_2 , in_3 , in_4 , sel_1 , sel_2 , out)
        input in_1 , in_2 , in_3 , in_4 , sel_1 , sel_2;
        output out;
        
        reg out;
        always @(in_1 , in_2 , in_3 , in_4 , sel_1 , sel_2)
        begin
            case()
    ```


#### 6.存储器：

- 我们先来谈一谈``固定逻辑器件``和``可编程逻辑器件PLD``。
  - 固定逻辑器件：顾名思义，这类器件的电路设计出来之后就不能改变，逻辑功能完全固定，这类器件适合大规模的进行生产。
  - 可编程逻辑器件PLD：这种逻辑器件比较神奇，我们通过硬件编程语言对电路的逻辑功能进行编程，然后将代码下载到这类逻辑器件中，逻辑器件就能够实现相应的电路功能，并且能够反复更改逻辑功能。使用PLD可以大大减少设计周期。
    - 在可编程逻辑器件的基础上，又产生了``现场可编程门阵列FPGA``。FPGA可以说是PLD的升级版，PLD最多只能提供一万门的逻辑资源，而FPGA能够提供大约八百万门的逻辑资源。
- 对FPGA等可编程逻辑器件来说，其内部都有自带的RAM资源，因此不推荐使用Verilog直接建模存储器。
- 既然不能直接建模RAM，那么如何使用这些内嵌的RAM资源呢？
  - 通过器件商提供的开发平台内嵌的IP生成器，在图形化界面直接选择存储器类型(如双口RAM、单口RAM、ROM、分布式RAM等)，然后配置存储器参数，生成相应的IP，直接调用即可。
  - 使用这种方式生成的存储器：方便、高效、可靠。
