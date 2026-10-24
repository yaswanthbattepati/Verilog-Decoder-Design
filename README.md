module dec_2x4_7_8_v(y,en,a,b);
input en,a,b;
output [3:0]y;
wire a_bar,b_bar;

not(a_bar,a);
not(b_bar,b);

and(y[0],en,a_bar,b_bar);
and(y[1],en,a_bar,b);
and(y[2],en,a,b_bar);
and(y[3],en,a,b);

endmodule


module dec_3x8_7_8(y,c,a,b);
input a,b,c;
output [7:0]y;
wire c_bar;
wire [3:0]y0,y1;

not(c_bar,c);

dec_2x4_7_8 D1(y0,c_bar,a,b);
dec_2x4_7_8 D2(y1,c,a,b);

assign y[3:0]=y0;
assign y[7:4]=y1;

endmodule


module dec_3x8_7_8_tb();
reg c,a,b;
wire [7:0]y;

dec_3x8_7_8 d(y,c,a,b);

initial
begin
c=0;a=0;b=0;#5
c=0;a=0;b=1;#5
c=0;a=1;b=0;#5
c=0;a=1;b=1;#5
c=1;a=0;b=0;#5
c=1;a=0;b=1;#5
c=1;a=1;b=0;#5
c=1;a=1;b=1;#5
$stop;
end
endmodule
