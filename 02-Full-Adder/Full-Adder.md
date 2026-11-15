# Full Adder

## Aim
To design a full adder using dataflow, gate-level and behavioral modeling styles.

## 1. Verilog design code

### Dataflow modeling
```verilog
module FA_Data(a, b, cin, sum, carry);
input a, b, cin;
output sum, carry;
assign sum = a ^ b ^ cin;
assign carry = (a & b) | (b & cin) | (a & cin);
endmodule
```

### Gate-level modeling
```verilog
module FA_gate(a, b, cin, sum, carry);
input a, b, cin;
output sum, carry;
wire s, t, u;
xor (s, a, b);
and (t, a, b);
xor (sum, s, cin);
and (u, s, cin);
or (carry, u, t);
endmodule
```

### Behavioral modeling (as printed in the manual)
```verilog
module FA_behavioral(a, b, cin, s, c);
input a, b, cin;
output reg s, c;
always @(a or b or cin)
begin
  if(a==0 & b==0 & cin==0) begin s=0; c=0; end
  else if(a==0 & b==0 & cin==1) begin s=1; c=0; end
  else if(a==0 & b==1 & cin==0) begin s=1; c=0; end
  else if(a==0 & b==1 & cin==1) begin s=0; c=1; end
  else if(a==1 & b==0 & cin==0) begin s=1; c=0; end
  else if(a==1 & b==0 & cin==1) begin s=0; c=1; end
  else if(a==1 & b==1 & cin==0) begin s=0; c=1; end
  else if(a==1 & b==1 & cin==1) begin s=1; c=1; end
end
endmodule
```

## 2. Verilog testbench code

This testbench targets the dataflow module `FA_Data`, with matching port names. The printed manual testbench uses `FA_behave`, which does not match the behavioral module name `FA_behavioral`; its signal names also differ. Use this matching testbench to simulate the dataflow module shown above.

```verilog
module FA_Test();
reg a, b, cin;
wire sum, carry;

FA_Data g1(a, b, cin, sum, carry);

initial
begin
  #0  a=1'b0; b=1'b0; cin=1'b0;
  #10 a=1'b0; b=1'b0; cin=1'b1;
  #10 a=1'b0; b=1'b1; cin=1'b0;
  #10 a=1'b0; b=1'b1; cin=1'b1;
  #10 a=1'b1; b=1'b0; cin=1'b0;
  #10 a=1'b1; b=1'b0; cin=1'b1;
  #10 a=1'b1; b=1'b1; cin=1'b0;
  #10 a=1'b1; b=1'b1; cin=1'b1;
end

initial
  $monitor($time, "a=%b, b=%b, cin=%b, sum=%b, carry=%b", a, b, cin, sum, carry);

initial
  #100 $finish;
endmodule
```
