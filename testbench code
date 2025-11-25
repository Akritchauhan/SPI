`timescale 1ns / 1ps

module tb_spi;

    reg clk = 0;
    reg start = 0;
    reg [11:0] din;
    wire cs, mosi, done, sclk;

    spi dut (
        .clk(clk),
        .start(start),
        .din(din),
        .cs(cs),
        .mosi(mosi),
        .done(done),
        .sclk(sclk)
    );

    integer i;

    initial begin
        #20;
        start = 1;

        for(i = 0; i < 10; i = i + 1) begin
            din = $urandom_range(0, 4095);
            @(posedge done);
            #10;
        end

        $stop;
    end

    always #5 clk = ~clk;

endmodule
