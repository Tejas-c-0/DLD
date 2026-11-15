# 1:4 Demultiplexer

## Aim
To design a 1:4 demultiplexer using a case statement.

## 1. Verilog design code
```verilog
module demux1to4(d, s, y);
input d;
input [1:0] s;
output reg [0:3] y;

always @ (*)
begin
  case(s)
    0: y={d, 3'b000};
    1: y={1'b0, d, 2'b00};
    2: y={2'b00, d, 1'b0};
    3: y={3'b000, d};
    default: y=4'b0000;
  endcase
end
endmodule
```

## 2. Verilog testbench code
```verilog
module demux1to4_tb();
reg d;
reg [1:0] s;
wire [0:3] y;

demux1to4 g1(d, s, y);

initial
begin
  #0  d=1'b0; s=2'b00;
  #10 d=1'b1; s=2'b00;
  #10 s=2'b01;
  #10 s=2'b10;
  #10 s=2'b11;
end

initial
  $monitor($time, "d=%b, s=%b, y=%b", d, s, y);

initial
  #100 $finish;
endmodule
```

**Manual note:** The printed testbench uses `End` with a capital E. Verilog keywords are case-sensitive, so it is written as `end` here.
