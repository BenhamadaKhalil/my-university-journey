# 📘 Chapter 3: Physical Layer – Math Rules Summary

## ✅ 1. Amplitude Modulation (AM)

**Formula:**

S(t)=a⋅cos⁡(ωt+ϕ)S(t) = a \cdot \cos(\omega t + \phi)

**Variables:**

- `S(t)` → Instantaneous signal [Volts]
    
- `a` → Amplitude of the signal [V]
    
- `\omega = 2\pi f` → Angular frequency [rad/s]
    
- `t` → Time [s]
    
- `\phi` → Phase [rad]
    
- `a_p` → Peak amplitude
    

---

## ✅ 2. Frequency Modulation (FM)

**Formulas:**

f=1/T,           ω=2πf,           S(t)=a⋅cos⁡(ωt+ϕ)                f = \frac{1}{T}, \quad \omega = 2\pi f, \quad S(t) = a \cdot \cos(\omega t + \phi)

**Variables:**

- `f` → Frequency [Hz]
    
- `T` → Period [s]
    
- `\omega` → Angular frequency [rad/s]
    

**Example:**

- Bit 0 → `f = f_p`
    
- Bit 1 → `f = 2f_p`
    

---

## ✅ 3. Phase Modulation (PM)

**Formula:**

S(t)=a⋅cos⁡(ωt+ϕ)              S(t) = a \cdot \cos(\omega t + \phi)

**Example:**

- Bit 1 → `\phi = \phi_p`
    
- Bit 0 → `\phi = \phi_p + \pi`
    

**Variables:**

- `\phi_p` → Reference phase [rad]
    

---

## ✅ 4. Bandwidth (W)

**Formula:**

W=f2−f1  W = f_2 - f_1

**Variables:**

- `W` → Bandwidth [Hz]
    
- `f_2` → Upper frequency limit [Hz]
    
- `f_1` → Lower frequency limit [Hz]
    

**Example:**

- `W = 3400 - 300 = 3100 Hz`
    

---

## ✅ 5. Symbol Rate (Baud Rate)

**Formula:**

R≤2W    R \leq 2W

**Variables:**

- `R` → Symbol rate [baud]
    
- `W` → Channel bandwidth [Hz]
    

---

## ✅ 6. Quantity of Information (Valence)

**Formula:**

Q=log⁡2(V)Q = \log_2(V)

**Variables:**

- `Q` → Bits per symbol [bits/symbol]
    
- `V` → Number of signal states (valence)
    

**Example:**

- `V = 4 → Q = \log_2(4) = 2 bits`
    

---

## ✅ 7. Signal-to-Noise Ratio (SNR)

**Formula (decibels):**

SNRdB=10⋅log⁡10(PSPN)SNR_{dB} = 10 \cdot \log_{10}\left(\frac{P_S}{P_N}\right)

**Variables:**

- `SNR_{dB}` → Signal-to-noise ratio [dB]
    
- `P_S` → Signal power [W]
    
- `P_N` → Noise power [W]
    

**Max Valence with Noise:**

Vmax=1+PSPNV_{max} = \sqrt{1 + \frac{P_S}{P_N}}

---

## ✅ 8. Maximum Bit Rate

### 🟩 Without Noise (Nyquist):

Dmax=2W⋅log⁡2(Vmax)    D_{max} = 2W \cdot \log_2(V_{max})

### 🟩 With Noise (Shannon):

Dmax=W⋅log⁡2(1+PSPN)D_{max} = W \cdot \log_2\left(1 + \frac{P_S}{P_N}\right)

**Variables:**

- `D_max` → Max bit rate [bps]
    
- `W` → Bandwidth [Hz]
    
- `V_max` → Maximum valence
    
- `P_S / P_N` → Signal-to-noise ratio (unitless)
    

---

## ✅ 9. Example – Shannon Capacity

**Given:**

- `W = 4000 Hz`
    
- `SNR_{dB} = 20 dB → \frac{P_S}{P_N} = 10^{2} = 100`
    

**Calculation:**

Dmax=4000⋅log⁡2(1+100)≈4000⋅6.6582=26632.8 bpsD_{max} = 4000 \cdot \log_2(1 + 100) \approx 4000 \cdot 6.6582 = 26632.8 \text{ bps}

---

✅ **Paste this directly into Obsidian** — it uses double-dollar `$$` blocks for math, which Obsidian renders perfectly if math mode is enabled.

Want it as flashcards or daily review prompts (like Obsidian + Anki)? Just say the word!