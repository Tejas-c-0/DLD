# 8:1 Multiplexer

## Aim
To design an 8:1 multiplexer using a case statement.

## 1. Verilog design code
```verilog
module mu8to1(i, s, y);
input [7:0] i;
input [2:0] s;
output reg y;

always @ (*)
begin
  case (s)
    3'b000: y=i[0];
    3'b001: y=i[1];
    3'b010: y=i[2];
    3'b011: y=i[3];
    3'b100: y=i[4];
    3'b101: y=i[5];
    3'b110: y=i[6];
    3'b111: y=i[7];
    default: y=1'b0;
  endcase
end
endmodule
```

## 2. Verilog testbench code
```verilog
module mux8to1_tb();
reg [7:0] i;
reg [2:0] s;
wire y;

mu8to1 g1(i, s, y);

initial
begin
  #0  s=3'b000; i=8'b10101010;
  #10 s=3'b001; i=8'b10101010;
  #10 s=3'b010; i=8'b10101010;
  #10 s=3'b011; i=8'b10101010;
  #10 s=3'b100; i=8'b10101010;
  #10 s=3'b101; i=8'b10101010;
  #10 s=3'b110; i=8'b10101010;
  #10 s=3'b111; i=8'b10101010;
end

initial
  $monitor($time, "i=%b, s=%b, y=%b", i, s, y);

initial
  #100 $finish;
endmodule
```

**Manual note:** The manual's default assignment is written as `y=8'b00000000`, although `y` is a 1-bit output. This page uses `1'b0` for the same default logic value.
