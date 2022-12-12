# 2.3 覆盖率检查

*   代码覆盖率

    > 代码覆盖率是检查代码执行完备性的重要指标，其中包括行line, fsm, toggle, branch和cond共5种覆盖率类型。

    *   行覆盖率(line)

        > 行覆盖率统计每一行代码的执行情况，统计公式为：$ line\_{cov} = \frac{lines\_of\_exec}{lines\_of\_total} $
    *   状态机覆盖率(fsm)

        > 状态机覆盖率统计状态转换的覆盖情况，统计公式为：$ fsm\_{cov} = \frac{trans\_of\_exec}{trans\_of\_total} $
    *   翻转覆盖率(toggle)

        > 翻转覆盖率统计端口/寄存器/变量中每一bit的翻转情况，包括1->0和0->1，统计公式为：$ toggle\_{cov} = \frac{toggle\_of\_exec}{toggle\_of\_total} $
    *   分支覆盖率(branch)

        > 分支覆盖率统计if..else if...else; case ... endcase中每个分支的执行情况，统计公式为: $ branch\_{cov} = \frac{branch\_of\_exec}{branch\_of\_total} $
    *   条件覆盖率(cond)

        > 条件覆盖率统计条件表达式的各种取值情况， $ cond\_{cov} = \frac{cond\_of\_exec}{cond\_of\_total} $
*   断言覆盖率

    > 断言是SystemVerilog新增的语言特性，一般用来检测信号级别的行为模式是否符合预期，下面举例：

    ```verilog
    // a上升沿后，再过3个时钟周期，b应为高
    property a_dly3_b;
        @(posedge clk) a |-> ##3 b;
    endproperty
    ```

    > 断言覆盖率就是统计代码中所有断言的覆盖情况，通过断言检查，可以轻松检查出波形难以发现的一些隐藏Bug。
*   功能覆盖率

    > 功能覆盖率统计用户定义的功能点的覆盖情况，功能覆盖点描述了spec中所有要求的特性，通过统计功能覆盖点的覆盖情况，可以很清晰地衡量一个设计的进度，一般要求功能覆盖率100%。

    ```verilog
    bit [7:0] a, b;
    covergroup odd_check @(posedge clk); // 在clk上升沿时采样覆盖率数据
        coverpoint a {
            bins odd_a = {a%2==0}; // 确保a的取值覆盖指定范围内(0~255)的所有偶数
        }
        coverpoint b {
            bins odd_b = {b%2==0}; // 确保b的取值覆盖指定范围内(0~255)的所有偶数
        }
    endgroup

    // testbench code
    initial begin
    	...
        odd_check inst_odd_check = new(); // initialize the covergroup
        ...
        $finish();
    end
    ```
