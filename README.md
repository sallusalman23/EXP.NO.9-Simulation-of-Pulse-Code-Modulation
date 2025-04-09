# EXP.NO.9-Simulation-of-Pulse-Code-Modulation

# AIM
To implement Pulse Code Modulation (PCM) using Python for a sinusoidal signal, including sampling, quantization, and encoding into binary form.

# SOFTWARE REQUIRED
Google colab

# ALGORITHMS
```
Start

Define the message signal parameters (frequency, duration, sampling rate).

Generate the message signal (e.g., sine wave).

Generate the clock signal (square wave).

Normalize the message signal to range 0 to 1.

Quantize the normalized signal into L levels.

Convert the quantized values into binary form (PCM encoding).

Flatten the binary values into a bitstream.

Plot:

Message signal

Clock signal

Quantized signal (PCM modulated)

Binary PCM signal (bitstream)

End
```
# PROGRAM
```
import numpy as np
import matplotlib.pyplot as plt

# Parameters
fs = 1000            # Sampling frequency (Hz)
f = 5               # Message frequency (Hz)
duration = 1         # Duration in seconds
L = 16                # Number of quantization levels (e.g., 4-bit PCM)

# Time vector
t = np.linspace(0, duration, int(fs * duration), endpoint=False)

# 1. Message Signal (Sine wave)
message = np.sin(2 * np.pi * f * t)

# 2. Clock Signal (Square wave)
clock = 0.5 * (1 + np.sign(np.sin(2 * np.pi * fs * t)))

# Normalize message to range 0-1
msg_norm = (message - message.min()) / (message.max() - message.min())

# 3. Quantization
quantized = np.round(msg_norm * (L - 1)) / (L - 1)

# 4. Encoding to binary
bits_per_sample = int(np.log2(L))
binary_data = [np.binary_repr(int(q * (L - 1)), width=bits_per_sample) for q in quantized]

# Convert binary data to PCM modulated signal (flattened bitstream for visualization)
bitstream = np.array([int(bit) for code in binary_data for bit in code])
time_pcm = np.linspace(0, duration, len(bitstream), endpoint=False)

# ----- PLOTS -----

plt.figure(figsize=(12, 8))

# Plot 1: Message signal
plt.subplot(4, 1, 1)
plt.plot(t, message, label="Message Signal", color='blue')
plt.title("1. Message Signal")
plt.xlabel("Time (s)")
plt.ylabel("Amplitude")
plt.grid(True)

# Plot 2: Clock signal
plt.subplot(4, 1, 2)
plt.plot(t, clock, label="Clock Signal", color='red')
plt.title("2. Clock Signal")
plt.xlabel("Time (s)")
plt.ylabel("Clock")
plt.ylim(-0.2, 1.2)
plt.grid(True)

# Plot 3: PCM Modulated Signal (Quantized)
plt.subplot(4, 1, 3)
plt.step(t, quantized, where='mid', label="PCM Quantized Signal", color='green')
plt.title("3. PCM Modulated Signal (Quantized)")
plt.xlabel("Time (s)")
plt.ylabel("Level")
plt.grid(True)

# Plot 4: PCM Signal without Demodulation (Bitstream)
plt.subplot(4, 1, 4)
plt.step(time_pcm, bitstream, where='post', label="PCM Bitstream", color='purple')
plt.title("4. PCM Bitstream (Without Demodulation)")
plt.xlabel("Time (s)")
plt.ylabel("Bit")
plt.ylim(-0.2, 1.2)
plt.grid(True)

plt.tight_layout()
plt.show()
```
# OUTPUT
![Screenshot 2025-04-09 181607](https://github.com/user-attachments/assets/3a55332f-c6f6-4e77-bf1f-1ca1f59e5d2a)

 
# RESULT / CONCLUSIONS
Pulse Code Modulation was successfully implemented using Python by sampling, quantizing, and encoding a sine wave signal. The PCM bitstream was generated without performing demodulation.
