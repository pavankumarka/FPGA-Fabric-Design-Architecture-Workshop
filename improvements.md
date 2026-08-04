## Improvements:

1. In Section 1.4: creates div_clk based counter design, this is not standard FPGA design practice, instead use "enable" based.

❌ Avoid div_clk <= ~div_clk; Good for understanding clock division
❌ Do not generate clocks in RTL using flip-flops or LUTs.
✅ Use clock enables: good for better FPGA design 
✅ Use dedicated clocking resources (PLL/MMCM/BUFG). Recommended when a true new clock is required
