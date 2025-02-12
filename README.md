# HDL_BITS
#vector----vector concatanation operator
#Vector3
assign {w,x,y,z}={a,b,c,d,e,f,2'b11};
assign out[24:20] = ~{5{a}} ^ {a,b,c,d,e};
    assign out[19:15] = ~{5{b}} ^ {a,b,c,d,e};
    assign out[14:10] = ~{5{c}} ^ {a,b,c,d,e};
    assign out[9:5] = ~{5{d}} ^ {a,b,c,d,e};
    assign out[4:0] = ~{5{e}} ^ {a,b,c,d,e};

#modules:hierarchy
#module shift8
module top_module ( 
    input clk, 
    input [7:0] d, 
    input [1:0] sel, 
    output [7:0] q 
);
    wire [7:0]w1;
    wire [7:0]w2;
    wire [7:0]w3;
    
    my_dff8 instance1 (.clk(clk), .d(d), .q(w1));
    my_dff8 instance2 (.clk(clk), .d(w1), .q(w2));
    my_dff8 instance3 (.clk(clk), .d(w2), .q(w3));
    
    always @(*)
        begin
        case (sel)
            0:q<=d;
            1:q<=w1;
            2:q<=w2;
            3:q<=w3;
        endcase
        end
endmodule
