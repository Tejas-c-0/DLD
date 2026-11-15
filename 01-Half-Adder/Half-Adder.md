# Half Adder

## Aim
To design a half adder using dataflow, gate-level and behavioral modeling styles.

## 1. Verilog design code

### Dataflow modeling
```verilog
module half_adder (
  input a,
  input b,
  output sum,
  output carry
);
assign sum = a ^ b;
assign carry = a & b;
endmodule
```

### Gate-level modeling
```verilog
module HA_gate(a, b, sum, carry);
input a, b;
output sum, carry;
xor (sum, a, b);
and (carry, a, b);
endmodule
```

### Behavioral modeling
```verilog
module half_adder_behave (
 input a,
 input b,
 output sum,
 output carry
);
reg sum, carry;
always @ (a or b)
begin
  sum = a ^ b;
  carry = a & b;
end
endmodule
```

## 2. Verilog testbench code

The manual's testbench instantiates the dataflow module `half_adder`.

```verilog
module HA_Test();
reg a, b;
wire sum, carry;

half_adder g1(a, b, sum, carry);

initial
begin
  #0  a = 1'b0; b = 1'b0;
  #30 a = 1'b0; b = 1'b1;
  #30 a = 1'b1; b = 1'b0;
  #30 a = 1'b1; b = 1'b1;
end

initial
  $monitor($time, "a = %b, b = %b, sum = %b, carry = %b", a, b, sum, carry);

initial
  #100 $finish;
endmodule
```
