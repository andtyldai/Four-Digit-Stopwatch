module HA(A,B,s,c);
    
    input A,B;
    output s,c;
    
    assign s = A^B;
    assign c = A&B;
    
endmodule
 
module RCA(I,i,s,c);
 
    input i;
    input [3:0]I;
    output [3:0]s;
    output c;
    wire [2:0]C;
 
    HA HA0(I[0],i,s[0],C[0]);
    HA HA1(I[1],C[0],s[1],C[1]);
    HA HA2(I[2],C[1],s[2],C[2]);
    HA HA3(I[3],C[2],s[3],c);
 
endmodule
 
module BCDto7SD(A, B, C, D, a, b, c, d, e, f, g);
 
    input A,B,C,D;
    output a, b, c, d, e, f, g;
 
    assign a = (B&~C&~D) | (~A&~B&~C&D);
 
    assign b = (B&~C&D) | (B&C&~D);
 
    assign c = (~B&C&~D);
 
    assign d = (B&~C&~D) | (~B&~C&D) | (B&C&D);
 
    assign e = (D) | (B&~C);
 
    assign f = (C&D) | (~A&~B&D) | (~B&C);
 
    assign g = (B&C&D) | (~A&~B&~C);
 
endmodule
 
module clk_divider(clock, rst, clk_out);
 
    input clock, rst;
    output clk_out;
    wire [18:0] din;
    wire [18:0] clkdiv;
 
    DFF0 dff_inst0(
        
        .data_in(din[0]),
        .clock(clock),
        .reset(rst),
        .data_out(clkdiv[0])
        
    );
 
    genvar i;
    generate
    
    for (i = 1; i < 19; i=i+1)
        
        begin : dff_gen_label
        
        DFF0 dff_inst (
            
            .data_in (din[i]),
            .clock(clkdiv[i-1]),
            .reset(rst),
            .data_out(clkdiv[i])
            
        );
        
        end
    
    endgenerate
    
    assign din = ~clkdiv;
    assign clk_out = clkdiv[18];
 
endmodule
 
module DFF0(data_in,clock,reset, data_out);
 
    input data_in;
    input clock,reset;
    output reg data_out;
 
    always@(posedge clock)
 
    begin
    
    if(reset)
    
    data_out<=1'b0;
    
    else
    
    data_out<=data_in;
    
    end
    
endmodule
 
module Reg(a, clock, reset, b);
    
    input [3:0] a;
    input clock, reset;
    output[3:0] b;
 
    DFF0 dff1(a[0], clock, reset, b[0]);
    DFF0 dff2(a[1], clock, reset, b[1]);
    DFF0 dff3(a[2], clock, reset, b[2]);
    DFF0 dff4(a[3], clock, reset, b[3]);
    
endmodule
 
module count6(clock, inc, reset, Count);
 
    input clock, inc, reset;
    output [3:0] Count;
    wire res;
    wire c;
    wire eq_count_5;
    wire [3:0] s;
 
    assign eq_count_5 = (Count == 4'b101) ? 1 : 0;
    assign res = (eq_count_5 & inc | reset);
    Reg Reg0(s, clock, res, Count);
    RCA RCA0(Count, inc, s, c);
 
endmodule
 
module count10(clock, inc, reset, Count);
 
    input clock, inc, reset;
    output [3:0] Count;
    wire res;
    wire c;
    wire eq_count_9;
    wire [3:0] s;
 
    assign eq_count_9 = (Count == 4'b1001) ? 1 : 0;
    assign res = (eq_count_9 & inc | reset);
    Reg Reg0(s, clock, res, Count);
    RCA RCA0(Count, inc, s, c);
 
endmodule
 
module FinalProject(inc, res, clock, a, b, c, d, e, f, g);
    
    input inc, res, clock;
    output [3:0]a, b, c, d, e, f, g;
    wire clock_out;
 
    clk_divider(clock, 0, clock_out);
    wire [3:0] Count0;
    wire [3:0] Count1;
    wire [3:0] Count2;
    wire [3:0] Count3;
    
    wire [2:0] carryover;
    
    assign carryover[0] = (Count0 == 4'b1001) ? 1 : 0;
    assign carryover[1] = (Count0 == 4'b1001 && Count1 == 4'b1001) ? 1 : 0;
    assign carryover[2] = (Count0 == 4'b1001 && Count1 == 4'b1001 && Count2 == 4'b1001) ? 1 : 0;
    
    count10(clock_out, inc, res, Count0);
    count10(clock_out, carryover[0], res, Count1);
    count10(clock_out, carryover[1], res, Count2);
    count6(clock_out, carryover[2], res, Count3);
    
    BCDto7SD(Count0[3], Count0[2], Count0[1], Count0[0], a[0], b[0], c[0], d[0], e[0], f[0], g[0]);
    BCDto7SD(Count1[3], Count1[2], Count1[1], Count1[0], a[1], b[1], c[1], d[1], e[1], f[1], g[1]);
    BCDto7SD(Count2[3], Count2[2], Count2[1], Count2[0], a[2], b[2], c[2], d[2], e[2], f[2], g[2]);
    BCDto7SD(Count3[3], Count3[2], Count3[1], Count3[0], a[3], b[3], c[3], d[3], e[3], f[3], g[3]);
 
endmodule
