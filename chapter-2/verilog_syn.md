## 2.1 Verilog可综合子集

-   模块声明

    ```verilog
    module module_name #(
    	// 参数声明
    )( 
        // 端口声明
    );
        // 内部信号 (reg/wire
        // 组合逻辑 (& | ~ ...)
        // 时许逻辑 (DFF)
    endmodule
    ```

-   端口声明

    ```verilog
    // 输入端口
    input 	wire 		rst_n;
    input 	wire [7:0] 	i_data;
    // 输出端口
    output 	wire 		o_txd ;
    output 	reg   [7:0]  o_data;
    // inout 端口
    inout 	wire 		sda   ;
    ```

-   参数定义

    ```verilog
    // 模块参数，可在模块例化时修改
    parameter WIDTH = 8;
    // 局部参数，只在模块内有效不能修改
    localparam TPER = 200;
    // 例化模块后，修改模块的参数
    mname inst(...);
    defparam inst.WIDTH = 8;
    ```

-   信号类型

    ```verilog
    // 连线类型, 用于组合逻辑中
    wire a,b,c;
    assign c = a & b;
    
    // reg类型，可用于组合逻辑和时许逻辑
    // 用于组合逻辑
    reg cnt_end;
    always @(*) begin
        ...
        cnt_end = (cnt>100);
    end
    
    // 用于时许逻辑
    reg [2:0] state, next_state;
    always @(posedge clk or negedge rst_n) begin
        if(~rst_n)
            state <= IDLE;
        else
            state <= next_state;
    end
    ```

-   控制流

    ```verilog
    // IF语句
    if(condition1) begin
        ...
    end 
    else if(condition2) begin
        ...
    end 
    else if(...) begin
    	...
    end 
    else begin
        ...
    end
    // CASE语句
    case(sel)
        0:
            ...
        1:
            ...
        ...
        default:
            ...
    endcase
    ```

-   循环语句

    ```verilog
    genvar j;
    generate
        for(j=0; j<N; j=j+1) begin: label
            // statement
            // module intialization
            // ...
        end
    endgenerate
    ```

    

-   赋值语句

    -   连续赋值

        ```verilog
        assign sum = a + b; // 只要输入a,b,发生变化，立刻重新计算sum
        ```

-   运算符

    -   赋值运算符

        -   阻塞赋值

            ```verilog
            // a=1, b=2, c=3
            a = b; // a --> 2
            c = a; // c --> 2
            ```

            >   1.   阻塞赋值的语句是顺序执行的
            >   2.   阻塞赋值一般用于组合逻辑中，包括assign和always @(*)
            >   3.   阻塞赋值时，左边的变量在语句执行结束后立即更新为新值

        -   非阻塞赋值

            ```verilog
            a <= b; // a --> 2
            c <= a; // c --> 1
            ```

            >   1.   非阻塞赋值的语句是并行执行的
            >   2.   非阻塞赋值一般用于时许逻辑中，如always @(posedge clk or negedge rst_n)
            >   3.   非阻塞赋值时，右边变量的值取的是前一时刻的旧值，而不是当前时刻获得的新值

    -   逻辑运算符

        -   单目运算符

            ```verilog
            |a, &a, ~a, ^a
            ```

        -   二元运算符

            ```verilog
            // a, b为多bit数据
            a && b, a || b
            // a, b为bool类型
            a & b, a | b, a ^ b
            ```

        -   三目运算符

            ```verilog
            a? b : c
            ```

    -   关系运算符

        ```verilog
        a==b, a>b, a<b, a>=b, a<=b
        ```

    -   移位运算符

        ```verilog
        // a: 0110 0010
        // 逻辑左移，低位补0
        a<<3 //0001 0000
        // 逻辑右移，高位补0
        a>>2 // 0001 1000
        ```

    -   拼接运算符

        ```verilog
        // a: 0011, b: 1010
        wire [7:0] c;
        assign c = {a,b}; // c: 0011 1010
        ```
