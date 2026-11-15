# 1:8 Demultiplexer

## Aim
To design a 1:8 demultiplexer using a case statement.

## 1. Verilog design code
```verilog
module demux1to8(y, s, a);
output reg [0:7] y;
input [2:0] s;
input a;

always @(*)
begin
  case(s)
    0: y={a, 7'b0000000};
    1: y={1'b0, a, 6'b000000};
    2: y={2'b00, a, 5'b00000};
    3: y={3'b000, a, 4'b0000};
    4: y={4'b0000, a, 3'b000};
    5: y={5'b00000, a, 2'b00};
    6: y={6'b000000, a, 1'b0};
    7: y={7'b0000000, a};
    default: y=8'b00000000;
  endcase
end
endmodule
```

## 2. Verilog testbench code
```verilog
module demux1to8_tb();
reg a;
reg [2:0] s;
wire [0:7] y;

demux1to8 g1(y, s, a);

initial
begin
  #0  a=1'b1; s=3'd0;
  #10 s=3'd1;
  #10 s=3'd2;
  #10 s=3'd3;
  #10 s=3'd4;
  #10 s=3'd5;
  #10 s=3'd6;
  #10 s=3'd7;
end

initial
  $monitor($time, "a=%b, s=%b, y=%b", a, s, y);

initial
  #100 $finish;
endmodule
```

**Manual note:** The printed testbench uses `End` with a capital E; corrected to the Verilog keyword `end`.
