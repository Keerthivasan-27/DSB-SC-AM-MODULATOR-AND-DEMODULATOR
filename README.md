# DSB-SC-AM-MODULATOR-AND-DEMODULATOR
## AIM:
To write a program to perform DSBSC modulation and demodulation using SCI LAB and study its spectral characteristics

## EQUIPMENTS REQUIRED
•	Computer with i3 Processor 
•	SCI LAB

Note: Keep all the switch faults in off position

## ALGORITHM:

1.	Define Parameters:
   
    •	Fs: Sampling frequency.
    
    •	T: Duration of the signal.
    
    •	Fc: Carrier frequency.
    
    •	Fm: Frequency of the message signal.
    
    •	Amplitude: Maximum amplitude of the message signal.

2.	Generate Signals:
 
  •	Message Signal: A sinusoidal signal that will be modulated.
  
  •	Carrier Signal: A high-frequency sinusoidal signal used for modulation.

3.	DSBSC Modulation:
   
  •	Modulated Signal: Multiply the message signal by the carrier signal to produce the DSBSC signal.

4.	DSBSC Demodulation:

  •	Multiplication: Multiply the modulated signal by the carrier signal to get the product of the message signal with itself (i.e., the original message signal plus high-frequency components).

  •	Low-pass Filtering: Apply a Butterworth low-pass filter to remove the high- frequency components and recover the original message signal.

5.	Visualization:
   
  Plot the message signal, carrier signal, DSBSC modulated signal, and the recovered signal after demodulation.

## PROCEDURE

  •	Refer Algorithms and write code for the experiment.
  
  •	Open SCILAB in System
  
  •	Type your code in New Editor
  
  •	Save the file
   
  •	Execute the code
  
  •	If any Error, correct it in code and execute again
  
  •	Verify the generated waveform using Tabulation and Model Waveform
  
## MODEL GRAPH:
<img width="503" height="479" alt="image" src="https://github.com/user-attachments/assets/9f4fdea5-8f1d-44ae-a75a-8c3737088c0a" />

## PROGRAM:
// DSB-SC AM MODULATOR
clc;
clear;
close;

// --- Parameters ---
Am = 2.3 + (124 * 0.1);     // 14.7
Ac = 29.4;                  // Carrier amplitude
fm = 213 + (124 * 10);      // 1453 Hz
fc = 14530;                 // Carrier frequency
fs = 145300;                // Sampling frequency (10x carrier)
t = 0:1/fs:3/fm;            // Duration for 3 message cycles

// --- Message and Carrier ---
m = Am * cos(2 * %pi * fm * t);    // Message signal
c = Ac * cos(2 * %pi * fc * t);    // Carrier signal

// --- DSB-SC Modulated Signal ---
s = m .* c;                        // Product modulation

// --- Plot ---
subplot(3,1,1);
plot(t, m);
title("Message Signal (m(t))");
xlabel("Time (s)");
ylabel("Amplitude");

subplot(3,1,2);
plot(t, c);
title("Carrier Signal (c(t))");
xlabel("Time (s)");
ylabel("Amplitude");

subplot(3,1,3);
plot(t, s);
title("DSB-SC Modulated Signal (s(t) = m(t)*c(t))");
xlabel("Time (s)");
ylabel("Amplitude");

// DSB-SC DEMODULATOR
clc;
clear;
close;

// --- Parameters ---
Am = 14.7;
Ac = 29.4;
fm = 1453;
fc = 14530;
fs = 145300;
t = 0:1/fs:3/fm;

// --- Message and Carrier ---
m = Am * cos(2 * %pi * fm * t);
c = Ac * cos(2 * %pi * fc * t);

// --- DSB-SC Modulated Signal ---
s = m .* c;

// --- Coherent Detection ---
local_carrier = cos(2 * %pi * fc * t);     // Local oscillator
y = s .* local_carrier;                    // Product demodulation

// --- Low-pass filtering using FFT method ---
Y = fft(y);
N = length(Y);
f = (0:N-1)*(fs/N);
cutoff = fc/2;                            // Keep frequencies below fc/2
H = (f < cutoff);
Y_filtered = Y .* H;
y_demod = real(ifft(Y_filtered));

// --- Plot ---
subplot(3,1,1);
plot(t, s);
title("Received DSB-SC Signal");
xlabel("Time (s)");
ylabel("Amplitude");

subplot(3,1,2);
plot(t, y);
title("After Coherent Mixing");
xlabel("Time (s)");
ylabel("Amplitude");

subplot(3,1,3);
plot(t, y_demod);
title("Demodulated Message Signal (After LPF)");
xlabel("Time (s)");
ylabel("Amplitude");



## TABULATION:

![WhatsApp Image 2025-11-19 at 19 36 58_84ab8b78](https://github.com/user-attachments/assets/794a21ed-7c91-4316-9eee-b4148cf0d4dd)

## OUTPUT:
![WhatsApp Image 2025-11-19 at 19 37 29_fcac1777](https://github.com/user-attachments/assets/4f1d9898-4bcf-4ba2-a174-d10afd9a82b6)

## RESULT:
Thus the DSB-SC-AM modulation and demodulation is generated and obtained the required output
