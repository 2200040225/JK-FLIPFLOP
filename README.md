# JK-FLIPFLOP

Design code:

module JK_FlipFlop (
    input J,   
    input K,    
    input clk,  
    input rst,  
    output reg Q, 
    output Qbar 
);
assign Qbar = ~Q;
always @(posedge clk or posedge rst)
begin
    if (rst)
        Q <= 1'b0; 
    else
    begin
        case ({J, K})
            2'b00: Q <= Q;      
            2'b01: Q <= 1'b0;  
            2'b10: Q <= 1'b1;   
            2'b11: Q <= ~Q;     
        endcase
    end
end
endmodule

Verilog code:

module JK_FlipFlop_tb();
    reg J, K, clk, rst;
    wire Q, Qbar;
    JK_FlipFlop uut (
        .J(J),
        .K(K),
        .clk(clk),
        .rst(rst),
        .Q(Q),
        .Qbar(Qbar)
    );
    always #5 clk = ~clk; 
    initial begin
        clk = 0;
        rst = 1; J = 0; K = 0;
        #10 
        rst = 0;
        #10 
        J = 0; K = 0;
        #10 
        J = 0; K = 1;
        #10 
        J = 1; K = 0;
        #10 
        J = 1; K = 1;
        #10 
        rst = 1;
        #5 
        rst = 0;
        #50 
        $stop;
    end
endmodule

