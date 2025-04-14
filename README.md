# EXP.NO.9-Simulation-of-Pulse-Code-Modulation
9.Simulation of PCM

# AIM:
To implement Pulse Code Modulation (PCM) using Python for a sinusoidal signal, including sampling, quantization, and encoding into binary form.

# SOFTWARE REQUIRED:
Google colab 

# ALGORITHMS:
# Sampling

1.The analog signal is sampled at regular intervals (usually according to the Nyquist rate, i.e., at least twice the maximum frequency in the signal).

2.This converts a continuous signal into a discrete-time signal.

# Quantization

1.Each sampled value is rounded off to the nearest value within a fixed set of levels.

2.This step introduces a small error known as quantization noise.

# Encoding

1.Each quantized value is then converted into a binary code.

2.The number of bits used depends on the desired resolution (e.g., 8-bit, 16-bit, 24-bit PCM).

# PROGRAM:
```
import numpy as np
import matplotlib.pyplot as plt  # Missing import added

# Parameters
sampling_rate = 5000  # Samples per second
frequency = 50  # Frequency of the analog message signal
duration = 0.1  # Duration in seconds
quantization_levels = 16  # Number of quantization levels

# Time vector
t = np.linspace(0, duration, int(sampling_rate * duration), endpoint=False)

# Message signal (sine wave)
message_signal = np.sin(2 * np.pi * frequency * t)

# Clock signal with increased frequency (200 Hz)
clock_signal = np.sign(np.sin(2 * np.pi * 200 * t))

# Quantization
quantization_step = (max(message_signal) - min(message_signal)) / quantization_levels
quantized_signal = np.round(message_signal / quantization_step) * quantization_step

# PCM encoding: normalize and convert to integers
pcm_signal = (quantized_signal - min(quantized_signal)) / quantization_step
pcm_signal = pcm_signal.astype(int)

# Plotting
plt.figure(figsize=(12, 10))

# 1. Message Signal
plt.subplot(4, 1, 1)
plt.plot(t, message_signal, label="Message Signal (Analog)", color='blue')
plt.title("Message Signal (Analog)")
plt.xlabel("Time [s]")
plt.ylabel("Amplitude")
plt.grid(True)

# 2. Clock Signal
plt.subplot(4, 1, 2)
plt.plot(t, clock_signal, label="Clock Signal (200 Hz)", color='green')
plt.title("Clock Signal (Increased Frequency)")
plt.xlabel("Time [s]")
plt.ylabel("Amplitude")
plt.grid(True)

# 3. PCM Modulated Signal (Quantized)
plt.subplot(4, 1, 3)
plt.step(t, quantized_signal, label="PCM Modulated Signal", color='red')
plt.title("PCM Modulated Signal (Quantized)")
plt.xlabel("Time [s]")
plt.ylabel("Amplitude")
plt.grid(True)

# 4. Simulated Demodulated Signal
plt.subplot(4, 1, 4)
plt.plot(t, quantized_signal, label="Demodulated Signal", color='purple', linestyle='--')
plt.title("Simulated Demodulated Signal")
plt.xlabel("Time [s]")
plt.ylabel("Amplitude")
plt.grid(True)

plt.tight_layout()
plt.show()
```

# OUTPUT:
![image](https://github.com/user-attachments/assets/ed6438f4-607c-4713-a647-d97e99626045)

 
# RESULT / CONCLUSIONS:
Thus the pulse code modulation converts an analog sine wave into a digital signal and the graph is obtained.
