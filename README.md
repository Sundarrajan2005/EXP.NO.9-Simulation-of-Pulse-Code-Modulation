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

# Parameters
sampling_rate = 8000
duration = 0.1
quantization_levels = 16

# Time base
t = np.linspace(0, duration, int(sampling_rate * duration), endpoint=False)

# Two message signals
frequency1 = 80
frequency2 = 160
message_signal1 = np.sin(2 * np.pi * frequency1 * t)
message_signal2 = np.sin(2 * np.pi * frequency2 * t)

# Quantization function
def quantize(signal, levels):
    step = (max(signal) - min(signal)) / levels
    quantized = np.round(signal / step) * step
    pcm = ((quantized - min(quantized)) / step).astype(int)
    return quantized, pcm

# Quantize both signals
quantized_signal1, pcm_signal1 = quantize(message_signal1, quantization_levels)
quantized_signal2, pcm_signal2 = quantize(message_signal2, quantization_levels)

# Multiplexing the PCM signals by interleaving
multiplexed_pcm = np.empty((pcm_signal1.size + pcm_signal2.size,), dtype=int)
multiplexed_pcm[0::2] = pcm_signal1
multiplexed_pcm[1::2] = pcm_signal2

# Time base for multiplexed signal
t_mux = np.linspace(0, duration, multiplexed_pcm.size, endpoint=False)

# Clock signal for reference
clock_signal = np.sign(np.sin(2 * np.pi * 200 * t))

# Plotting
plt.figure(figsize=(14, 12))

plt.subplot(8, 1, 1)
plt.plot(t, message_signal1, label="Message Signal 1 (50Hz)", color='blue')
plt.title("Original Message Signal 1")
plt.xlabel("Time [s]")
plt.ylabel("Amplitude")
plt.grid(True)
plt.legend()

plt.subplot(8, 1, 2)
plt.plot(t, clock_signal, label="Clock Signal", color='green')
plt.title("Clock Signal")
plt.xlabel("Time [s]")
plt.ylabel("Amplitude")
plt.grid(True)
plt.legend()

plt.subplot(8, 1, 3)
plt.step(t, quantized_signal1, label="Quantized Signal 1", color='red')
plt.title("Quantized Signal 1")
plt.xlabel("Time [s]")
plt.ylabel("Amplitude")
plt.grid(True)
plt.legend()

plt.subplot(8, 1, 4)
plt.plot(t, message_signal2, label="Message Signal 2 (120Hz)", color='orange', alpha=0.7)
plt.title("Original Message Signal 2")
plt.xlabel("Time [s]")
plt.ylabel("Amplitude")
plt.grid(True)
plt.legend()

plt.subplot(8, 1, 5)
plt.plot(t, clock_signal, label="Clock Signal", color='green')
plt.title("Clock Signal")
plt.xlabel("Time [s]")
plt.ylabel("Amplitude")
plt.grid(True)
plt.legend()

plt.subplot(8, 1, 6)
plt.step(t, quantized_signal2, label="Quantized Signal 2", color='purple', alpha=0.7)
plt.title("Quantized Signal 2")
plt.xlabel("Time [s]")
plt.ylabel("Amplitude")
plt.grid(True)
plt.legend()

plt.subplot(8, 1, 7)
plt.step(t, quantized_signal1, label="Quantized Signal 1", color='red')
plt.step(t, quantized_signal2, label="Quantized Signal 2", color='purple', alpha=0.7)
plt.title("Overlay of Quantized Signals")
plt.xlabel("Time [s]")
plt.ylabel("Amplitude")
plt.grid(True)
plt.legend()

plt.subplot(8, 1, 8)
plt.step(t_mux, multiplexed_pcm, label="Multiplexed PCM Signal", color='black')
plt.title("Multiplexed PCM Signal (Interleaved)")
plt.xlabel("Time [s]")
plt.ylabel("PCM Value")
plt.grid(True)
plt.legend()

plt.tight_layout()
plt.show()
```

# OUTPUT:
![image](https://github.com/user-attachments/assets/eef0c2a5-625f-4a5f-bb9e-07bf5ff66b3f)

 
# RESULT / CONCLUSIONS:
Thus the pulse code modulation converts an analog sine wave into a digital signal and the graph is obtained.
