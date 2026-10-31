extras/virtual_zedboard.html  -  Virtual ZedBoard (teaching simulation)
=====================================================================
A single self-contained HTML file. Open it in any browser; no install, no server.
It is a SOFTWARE SIMULATION written for learning. It is NOT the physical board,
NOT connected to Vivado/Vitis, and NOT evidence of a hardware run. The evidence
for the lab is the Vivado testbenches (sim/), the C model (sw/main_sim.c) and the
implementation reports (reports/).

What is on the page
-------------------
Board        8 LEDs, 8 clickable switches, presets, BTNC (hold to press), optional
             contact bounce, ISR debounce version A (as built) or B (recommended).
Lessons      7 guided steps. Each says what to try and ticks itself off when you do it:
             switch -> brightness, why 128 = 50 %, BTNC interrupt, contact bounce,
             breathing curve, slow-motion counter, debounce experiment A vs B.
Tabs         Console & scope    UART lines ("Mode: BREATHING | Duty: 128"), registers, LD0 waveform
             Show me the math   switch value -> duty -> threshold = d*PERIOD/256 -> high time,
                                live, plus a calculator for your own numbers
             Slow motion        one period drawn as 64 steps: counter, threshold, output pin
             Code               BtnIsr(), main loop, pwm_set_all(); executing lines light up
             Register writes    each AXI write decoded (e.g. 0x08 DUTY_LO <- 0x80808080) with its cause
             System             clickable block diagram, wires light as they are used
             Check yourself     8 questions with instant feedback
             Glossary & limits  terms, and a table "this page vs real board"
Time scale   Real design (PERIOD 100000, 1 kHz) or Testbench (PERIOD 1000, 100 kHz).

Model rules (same as the RTL)
-----------------------------
threshold = floor(d * PERIOD / 256); d = 255 is always on. 128 -> 50 %, 64 -> 25 %, 100 -> 39 %.
ISR: toggle mode on a press only if the button was quiet for 100 ms.
Breathing: duty = breath*breath/255, +/-1 every 4 ms.

Tested in Chromium (Playwright): all lesson checks, switches, BTNC with and without
bounce, both ISR versions, quiz, scale toggle, 390 px phone width, no console errors.
The page loads fonts from Google Fonts if online and falls back to system fonts offline.
