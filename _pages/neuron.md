---
layout: page
permalink: /neuron/
title: GHK
description: flag{pK_pNa_pCl}
nav: false
---
## Neuron simulation

<div style="margin-top:20px; padding:15px; border:1px solid #ccc;">
  <h3>Neuron Challenge</h3>

  <p>Enter ion concentrations (in mM):</p>

  <label> [K+]<sub>out</sub> </label>
  <input id="k_out" type="number" step="0.1" value="5"><br><br>

  <label> [K+]<sub>in</sub> </label>
  <input id="k_in" type="number" step="0.1" value="140"><br><br>

  <label> [Na+]<sub>out</sub> </label>
  <input id="na_out" type="number" step="0.1" value="145"><br><br>

  <label> [Na+]<sub>in</sub> </label>
  <input id="na_in" type="number" step="0.1" value="12"><br><br>

  <label> [Cl–]<sub>out</sub> </label>
  <input id="cl_out" type="number" step="0.1" value="110"><br><br>

  <label> [Cl–]<sub>in</sub> </label>
  <input id="cl_in" type="number" step="0.1" value="4"><br><br>

  <button onclick="computeVoltage()" style="padding:6px 12px;">Submit</button>

  <p id="output" style="margin-top:15px; font-weight:bold;"></p>
</div>

<script>
// Constants
const R = 8.314;      // J/(mol*K)
const T = 310;        // K (37°C)
const F = 96485;      // C/mol


const gk = 1.0;
const gna = 0.04;
const gcl = gk - 0.55;


function computeVoltage() {
    const k_out = parseFloat(document.getElementById("k_out").value);
    const k_in  = parseFloat(document.getElementById("k_in").value);
    const na_out = parseFloat(document.getElementById("na_out").value);
    const na_in  = parseFloat(document.getElementById("na_in").value);
    const cl_out = parseFloat(document.getElementById("cl_out").value);
    const cl_in  = parseFloat(document.getElementById("cl_in").value);

    // GHK
    const numerator = (gk * k_out) + (gna * na_out) + (gcl * cl_in);
    const denominator = (gk * k_in) + (gna * na_in) + (gcl * cl_out);

    const Vm = (R * T / F) * Math.log(numerator / denominator) * 1000;

    const output = document.getElementById("output");
    output.textContent = "Computed Vm = " + Vm.toFixed(2) + " mV";

    output.style.color = "green";

}
</script>
