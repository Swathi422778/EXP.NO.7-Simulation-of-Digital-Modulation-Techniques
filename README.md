# EXP.NO.7-Simulation-of-Digital-Modulation-Techniques


# AIM
 i) Amplitude Shift Keying (ASK)
ii) Frequency Shift Keying (FSK)
iii) Phase Shift Keying (PSK)

# SOFTWARE REQUIRED
Google Colab

# ALGORITHMS

Start

Input binary data (example: [1, 0, 1, 1, 0])

Set parameters:

Bit rate

Sampling rate

Bit duration = 1 / bit rate

Carrier frequency (fc)

FSK frequencies: f1 (for bit 1), f0 (for bit 0)

ASK amplitudes: A1 (bit 1), A0 (bit 0)

For each bit in the binary data:

Generate digital square wave (1 or 0)

Generate ASK signal:

Use A1 * sin(2πfct) for bit 1

Use A0 * sin(2πfct) for bit 0

Generate FSK signal:

Use sin(2πf1t) for bit 1

Use sin(2πf0t) for bit 0

Generate PSK signal:

Use sin(2πfct) for bit 1

Use sin(2πfct + π) for bit 0

Combine all bit signals into full-length ASK, FSK, PSK signals

Plot:

Digital input signal

ASK modulated signal

FSK modulated signal

PSK modulated signal

End
# PROGRAM
```
import numpy as np
import matplotlib.pyplot as plt

# Input binary data
data = [1, 0, 1, 1, 0, 1]

# Parameters
bit_rate = 1          # bits per second
fs = 1000             # sampling frequency (samples per second)
Tb = 1 / bit_rate     # time per bit
t_bit = np.linspace(0, Tb, int(fs * Tb), endpoint=False)  # time vector for one bit

# Carrier settings
fc = 10  # Carrier frequency for ASK/PSK
f1 = 10  # Frequency for FSK - bit 1
f0 = 5   # Frequency for FSK - bit 0
A1 = 1   # Amplitude for bit 1
A0 = 0   # Amplitude for bit 0 (ASK 0)

# Empty lists to build signals
digital_signal = []
ask = []
fsk = []
psk = []

# Modulation and digital signal generation
for bit in data:
    # Digital signal (square wave)
    digital_bit = np.ones_like(t_bit) * bit
    digital_signal.extend(digital_bit)

    # ASK modulation
    ask_bit = (A1 if bit == 1 else A0) * np.sin(2 * np.pi * fc * t_bit)
    ask.extend(ask_bit)

    # FSK modulation
    fsk_freq = f1 if bit == 1 else f0
    fsk_bit = np.sin(2 * np.pi * fsk_freq * t_bit)
    fsk.extend(fsk_bit)

    # PSK modulation
    phase = 0 if bit == 1 else np.pi
    psk_bit = np.sin(2 * np.pi * fc * t_bit + phase)
    psk.extend(psk_bit)

# Full time axis
t_total = np.linspace(0, Tb * len(data), int(fs * Tb * len(data)), endpoint=False)

# Plotting
plt.figure(figsize=(14, 10))

plt.subplot(4, 1, 1)
plt.plot(t_total, digital_signal, color='black')
plt.title("Digital Input Signal")
plt.ylabel("Amplitude")
plt.ylim(-0.5, 1.5)
plt.grid(True)

plt.subplot(4, 1, 2)
plt.plot(t_total, ask, color='blue')
plt.title("Amplitude Shift Keying (ASK)")
plt.ylabel("Amplitude")
plt.grid(True)

plt.subplot(4, 1, 3)
plt.plot(t_total, fsk, color='orange')
plt.title("Frequency Shift Keying (FSK)")
plt.ylabel("Amplitude")
plt.grid(True)

plt.subplot(4, 1, 4)
plt.plot(t_total, psk, color='green')
plt.title("Phase Shift Keying (PSK)")
plt.xlabel("Time (s)")
plt.ylabel("Amplitude")
plt.grid(True)

plt.tight_layout()
plt.show()
```

# OUTPUT
![image](https://github.com/user-attachments/assets/69f0ed3c-acfc-406a-bcff-c55219022317)

 
# RESULT / CONCLUSIONS
The simulation of digital modulation techniques such as ASK, FSK, and PSK was successfully implemented using Python. The differences between amplitude, frequency, and phase modulation were clearly observed in the plotted waveforms.
