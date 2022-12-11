## 2.2 组合逻辑与时序逻辑

-   组合逻辑

    >   组合逻辑的输出由输入经过一系列逻辑运算得到，且当输入发生变化时，输出会立即更新当前状态；

    ```verilog
    // 连续赋值实现与运算
    assign c = a & b;
    
    // always block实现与运算
    reg c; // always块中被赋值的变量必须是reg类型，但不一定被综合成真正的寄存器
    always @(*) begin
        c = a & b;
    end
    ```

-   时许逻辑

    >   时序逻辑由典型的组合逻辑＋触发器构成，时序逻辑具有记忆性，能够保存组合逻辑的运算结果，同时输出也可能反馈回组合逻辑的输入，具体根据实际应用决定。

    ```verilog
    // 组合逻辑负责实现功能运算
    assign c = a & b | out; 
    // 触发器赋值保存运算结果，并反馈至组合逻辑的输入
    reg out;
    always @(posedge clk or negedge rst_n) begin
        if(~rst_n)
            out <= 1'b0;
        else
            out <= c ^ (a | b);
    end
    ```

    

    