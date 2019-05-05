# CETAL calculation

## CPLS parameters

The Ti:Sapph CETAL-PW Laser System (CPLS) has a wavelength $\lambda_L = 800$ nanometers. The focal length of its off-axis parabolic mirror (OAP) is 3.2 meters, while the beam size is 200 millimeters. We can take the pulse duration to be $\tau_L = 40$ fs at FWHM in intensity. 

## Electron acceleration estimate

For optimal acceleration, we impose the condition that the dephasing length should be equal to the pump depletion length $L_{\text{dephasing}} = L_{\text{depletion}}$. 

$$L_{\text{dephasing}} = \frac{4}{3} \left(\frac{\omega_L}{\omega_p}\right)^2 \frac{\sqrt{a_0}}{k_p} = L_{\text{depletion}} = \left(\frac{\omega_L}{\omega_p}\right)^2 c \tau_L$$

In practical units, we have $\lambda_p [\mu \text{m}] = 3.34 \times 10^{10} (n_p [\text{cm}^{-3}])^{-1/2}$, therefore $k_p [\mu \text{m}^{-1}]= 2\pi / \lambda_p  [\mu \text{m}] = 1.88 \times 10^{-10}  (n_p [\text{cm}^{-3}])^{1/2}$ and $\omega_p [\text{fs}^{-1}] = 5.64 \times 10^{-11} (n_p [\text{cm}^{-3}])^{1/2}$. 
This allows us to obtain the ratio $a_0/n_p$ from above.

$$\frac{a_0}{n_p [\text{cm}^{-3}]} = 1.79 \times 10^{-21} (\tau_L [\text{fs}])^2$$

### Plasma density and normalized vector potential
If we want to use any external guiding (eg via capilaries), then we also need to impose the condition for self-guided propagation of the laser:

$$a_0 \geq \left(\frac{n_c}{n_p}\right)^{1/5}$$

with the critical density $n_c [\text{cm}^{-3}] = 1.12 \times 10^{21} / (\lambda_L [\mu\text{m}])^2$, which is $1.75 \times 10^{21} \text{cm}^{-3}$ in our case. Substituting above and taking the lower limit, we get

$$n_p [\text{cm}^{-3}] = \frac{1.12 \times 10^{21} }{a_0^5 (\lambda_L [\mu\text{m}])^2}$$

Substituting $n_p$ in the ratio $a_0/n_p$ from above, we finally get:

$$a_0 \approx 2^{1/6} \left( \frac{\tau_L [\text{fs}]}{\lambda_L [\mu\text{m}]} \right)^{1/3} $$

and 

$$n_p [\text{cm}^{-3}] = 6.29 \times 10^{20} \frac{1}{(\lambda_L [\mu\text{m}])^{1/3} (\tau_L [\text{fs}])^{5/3}}$$

For CPLS parameters, we get $a_0 \approx 4.2$ and $n_p \approx 1.5 \times 10^{18} \text{cm}^{-3} = 8.57 \times 10^{-4} n_c$. For $a_0 \geq 4-5$ we also get self-injection from pure Helium. Helium has the ionization energies 24.59 eV (He${}^{+}$) and 54.42 (He${}^{2+}$), corresponding to laser intensities $1.4 \times 10^{15}$, respectively $8.8 \times 10^{15}$ W/cm${}^2$ (Gibbon, "Short pulse laser interactions with matter", p. 22), and will therefore be easily ionized by the laser prepulse.
Knowing the density, we get $\omega_p = 6.91 \times 10^{-2}$ fs${}^{-1}$, and more importantly, $\omega_p^{-1} = 14.48$ fs, which is the same order of magnitude as the pulse duration $\tau_L = 40$ fs. For $\tau_L \gg \omega_p^{-1}$ (eg. $\tau_L = 600$ fs), one would either be in the SMLWFA or DLA regime, depending on the value of $a_0$.

### Beam waist
We also need to match the beam waist $w_0$ of the focused Gaussian laser pulse to the plasma, giving the condition $w_0 k_p = 2 \sqrt{a_0}$, so

$$w_0 [\mu \text{m}] = 1.06 \times 10^{10}   \left(\frac{a_0}{n_p [\text{cm}^{-3}]}\right)^{1/2} = 44.84  \frac{\tau_L [\text{fs}]}{100}$$

For CPLS, we get $w_0 \approx 18 \mu \text{m}$ at $1/e^2$ intensity, so FWHM (1/2 intensity) = $w_0 \sqrt{2 \ln{2}} \approx 21 \mu$m. The realistic value, according to Liviu, is $25 \mu \text{m}$ and the diffraction-limited value according to *CALCTOOL* is $16 \mu \text{m}$.

### Laser energy, power and intensity 
We now estimate the required laser energy $\varepsilon_L$. The peak laser intensity in the focal plane is 

$$I_L [10^{18} \text{W}/\text{cm}^2 ] \approx 6 \times 10^4  \frac{\varepsilon_L [\text{J}]}{\tau_L [\text{fs}] (w_0 [\mu \text{m}])^2}$$

so for our parameters $I_L \approx 3.56 \times 10^{19}$ W/cm${}^2$. For a relative scale, the atomic Coulomb field is on the order of $10^{14}$ W/cm${}^2$ and relativistic effects become important for laser intensities above $10^{17}$ W/cm${}^2$ ($a_0 \geq 1$), while QED effects such as radiation reaction only become important for intensities beyond $\sim 2 \times 10^{21}$ W/cm${}^2$.
We know that $a_0 = 0.855 \lambda_L [\mu\text{m}] (I_L [10^{18} \text{W}/\text{cm}^2 ])^{1/2}$, so

$$\varepsilon_L [\text{J}] = 2.28 \times 10^{-5} a_0^2 (w_0 [\mu \text{m}])^2 \frac{\tau_L [\text{fs}] }{(\lambda_L [\mu\text{m}])^2} = 5.68 \times 10^{-6} \frac{ (\tau_L [\text{fs}])^{11/3} }{(\lambda_L [\mu\text{m}])^{8/3}}$$

Therefore, for CPLS we need $\varepsilon_L \approx 7.7$ J on target. If we assume the laser energy before the compressor is 20 J, and 30% is lost in the compressor and beam transport, we are left with 14 J in the chamber. If 50% of this energy can be focused into the FWHM spot of $21 \mu$m, we get 7 J on target.

The laser power on target is  

$$P [\text{TW}] = 2.41 \times 10^{18}   \frac{a_0^3}{n_p [\text{cm}^{-3}]} \frac{1}{(\lambda_L [\mu\text{m}])^2}$$

$$P [\text{TW}] = 2 \times 10^3 \sqrt{\frac{\ln{2}}{\pi}} \frac{1}{\tau_L [\text{fs}]} \varepsilon_L [\text{J}] = 5.34 \times 10^{-3} \left(\frac{ \tau_L [\text{fs}] }{\lambda_L [\mu\text{m}]}\right)^{8/3}$$

so approximately 180 TW in our case.

### Acceleration distance
The optimum propagation distance is equal to $L = L_{\text{dephasing}} (= L_{\text{depletion}})$. 

$$L [\text{mm}] = 3.34 \times 10^{17} \frac{\tau_L[\text{fs}]}{ (\lambda_L [\mu\text{m}])^2} \frac{1}{n_p [\text{cm}^{-3}]} = 5.31 \times 10^{-4} \frac{(\tau_L [\text{fs}])^{8/3}}{ (\lambda_L [\mu\text{m}])^{5/3}}$$

which for CPLS amounts to $L \approx 14$ mm.

### Maximum electron energy and charge
The maximum electron energy that can be reached under these circumstances is 

$$\gamma = \frac{\Delta \varepsilon}{mc^2} = \frac{2}{3} a_0 \frac{\omega_L^2}{\omega_p^2}$$

$$\gamma = 7.44 \times 10^{20} \frac{a_0}{n_p [\text{cm}^{-3}]} \frac{1}{ (\lambda_L [\mu\text{m}])^2 } = 1.33 \left(\frac{\tau_L [\text{fs}]}{ \lambda_L [\mu\text{m}] }\right)^2 $$

$$\Delta \varepsilon [\text{GeV}]= 5.11 \times 10^{-4} \gamma = 6.8 \times 10^{-4} \left(\frac{\tau_L [\text{fs}]}{ \lambda_L [\mu\text{m}] }\right)^2$$

For CPLS, we get $\Delta \varepsilon = 1.7$ GeV and a Lorentz factor $\gamma = 3325$. 

We assume the blowout radius $R = w_0 = 44.84 \tau_L [\text{fs}]/100 = 18 \, \mu$m. The number of accelerated electrons $N_e \propto R^3 n_p$ is equal to the ionic charge of the bubble, so (Lu et. al, 2007)

$$N_e \approx 3.13 \times 10^8 \lambda_L [\mu\text{m}] \left(P [\text{TW}]\right)^{1/2} = 2.28 \times 10^7  \frac{ (\tau_L [\text{fs}])^{4/3} }{ (\lambda_L [\mu\text{m}])^{1/3} }$$ 

$$N_e \approx 4.85 \times 10^{17}   \frac{a_0^{3/2}}{(n_p [\text{cm}^{-3}])^{1/2}} $$

giving a charge

$$Q_e [\text{pC}] = N_e \times e [\text{pC}] \approx 3.65  \frac{ (\tau_L [\text{fs}])^{4/3} }{ (\lambda_L [\mu\text{m}])^{1/3} } $$

For CPLS we get $Q_e \approx 540 \, \text{pC} \approx 0.5$ nC and $N_e = 3.36 \times 10^9$ electrons.
As a last note, with PW lasers, the higher laser energy can be focused to a larger focal spot matched by a lower plasma density.

### External guiding
- [ ] adapt to CETAL parameters

3J, $a_0 = 2$, $n_p = 5.1 \times 10^{17}$ cm${}^{-3}$, $w_0 = 21\, \mu\text{m}$, $\tau_L = 47\, \text{fs}$
- needs external guiding (capilaries)
- needs external injection
- can reach $\Delta \varepsilon = 2.4$ GeV after 52 mm of plasma


## Betatron emission
After matching the laser spot size, and pulse duration to the plasma density, we can look at betatron emission.
The betatron oscillation radius $r_{\beta} = 3\, \mu$m for a blowout radius $R = 21 \, \mu$m. Since the betatron oscillations are limited by the bubble size, it is reasonable to assume a linear dependence on $R$ and therefore take $r_{\beta} = 2.6 \, \mu$m in our case.

We now need to work out the five relevant parameters for the wiggler: the relativistic electron factor $\gamma$, the number of electrons $N_e$, the strength parameter $K$, the period of the wiggler $\lambda_u$ and the number of (betatron) periods $N$. We already know the first two parameters. Once we have the parameters, we can calculate the critical radiation energy $\hbar \omega_c$, the opening angle of the radiation $\theta_r$ and the number of emitted photons per electron and per betatron period, $N_{\gamma}$. We can then get the total number of emitted photons per laser shot, $N_{\gamma} \times N_e \times N$.

$$\theta_r [\text{mrad}] = 10^3 \times \frac{K}{\gamma} $$
$$N_{\gamma} = 3.31 \times 10^{-2} K$$
$$\hbar \omega_c [\text{keV}] = 1.86 \times 10^{-3} \frac{K \gamma^2}{\lambda_u [\mu\text{m}]}$$

### Wiggler parameters
In the case of betatron oscillations, the strength parameter is given by

$$K = \sqrt{\frac{\gamma}{2}} \left(k_p [\mu\text{m}^{-1}]\right) (r_{\beta} [\mu\text{m}]) = 1.33 \times 10^{-10} r_{\beta} [\mu\text{m}] (\gamma \, n_p [\text{cm}^{-3}])^{1/2} $$

so $K \approx 25$ in our case, which puts us in the wiggler regime $K \gg 1$.

$$\lambda_u [\mu\text{m}]= \sqrt{2} \gamma^{1/2} (\lambda_p [\mu\text{m}]) = 4.72 \times 10^{10}  \left(\frac{\gamma}{n_p [\text{cm}^{-3}]}\right)^{1/2}$$

so $\lambda_u = 2222 \, \mu\text{m} = 2.22$ mm. 

### Radiation properties
We now easily obtain $\theta_r = 8$ mrad and $N_{\gamma} = 0.8$ photons / (electron x betatron period). While the electrons radiate throughout the whole acceleration process, theefficiency main contribution comes from the part of the trajectory where their energy is maximum, ie, after the distance $L$. If the electron is around its maximum energy for about $N \sim 3$ betatron periods, the total number of emitted photons per shot will be $N_{\gamma}^{\text{shot}} = N_{\gamma} \times N_e \times N = 0.8 \times 3.36 \times 10^9 \times 3 \approx 8 \times 10^9$ photons. Finally, the critical energy is in our case $\hbar \omega_c = 230$ keV.

**Note:** The betatron amplitude $r_{\beta} \propto \sqrt{a_0/n_p}$ and the numer of betatron oscillations $N \propto 1/\sqrt{n_p}$.




## Quantum effects
We are now ready to estimate the size of the quantum corrections. Quantum effects become important when the electron energy loss due to photon emission becomes comparable to the electron energy.

### Nonlinear quantum parameter
We first look at the so-called nonlinear quantum parameter $\chi_0$ defined in (Di Piazza et al., 2012) for the case of an ultrarelativistic electron counter-propagating with respect to a plane wave:

$$\chi_0 = 5.9 \times 10^{-3} \Delta \varepsilon [\text{GeV}]  (I_L [10^{18} \text{W}/\text{cm}^2] )^{1/2}$$

giving $\chi_0 \approx 6 \times 10^{-2}$. $\chi_0$ can be interpreted as the aplitude of the plane wave's electric field in the electron rest frame (in units of the critical QED field $m^2/e = 1.3 \times 10^{16}$ V/cm $= 1.3 \times 10^6$ TV/m) and controld quantum effects such as photon recoil and spin. Since $\chi_0 \ll 1$, these effects play a minor role here. In fact our electric field is just $E_L [\text{TV/m}] = 3.21 a_0 / \lambda_L [\mu\text{m}] = 0.169$ TV/cm. Inside the plasma, the maximum accelerating field achievable at a given plasma density is $\approx a_0^{1/2}E_0$ (for $a_0 \geq 2$), where $E_0$ is the cold nonrelativistic wave-breaking field, $E_0 [\text{V/cm}] \approx 0.96 (n_p [\text{cm}^{-3}])^{1/2}$. In our case $a_0^{1/2}E_0 = 2.41 \times 10^9$ V/cm.

### Interaction duration
The other way to estimate quantum effects is by following (Corde et al., 2013), which explains that radiation reaction can be neglected when the electron - laser interaction duration is much smaller than the electron energy loss rate, or equivalently, the number of oscillations $N \ll N_{\text{RR}}$, with

$$N_{\text{RR}} = 2.7 \times 10^7 \frac{\lambda_u [\mu\text{m}]}{\gamma K^2}$$

so for CPLS parameters $N_{\text{RR}} \sim 2.9 \times 10^4 \gg N$.

## Multiple stages
- [ ] explain why people look at 2-stage solution 
	- [ ] see slack chat with Igor

## Computational resources
- [ ] estimate computational resources for PIC based on these parameters
	- [ ] PIConGPU Python memory calculator
	- [ ] png collage


# GBS calculation
## GBS parameters
The Gamma Beam System (GBS) consists of a 0.1 TW, 0.4 J, 3.5 ps FWHM Yb:Yag laser system operating at its second harmonic $\lambda_L = 515$ nm (0.1%BW) and a linear electron accelerator (LINAC) of average current $0.75 \, \mu$A. The photons from the laser are scattered by electrons from the LINAC, which have a tunable energy in the range 80-720 MeV at 0.1%BW. The electrons come in trains which are 10 ms apart (100 Hz LINAC rep rate), and each train contains 32 bunches separated by 16 ns. The bunches have a charge $Q_e = 250$ pC and a length between 100 and 400 $\mu$m, while their focal spot size is 15 $\mu$m. By use of a recirculator, the same laser pulse can interact with all 32 electron bunches in a train before being dumped, resulting in an "effective" laser repetition rate of 3.2 kHz. At the interaction points, the laser beam waist is $w_0 = 28 \, \mu$m, resulting in $I_L = 8.7 \times 10^{15}$ W/cm${}^2$.[^1] For the following, we will consider the electrons to be at the maximum LINAC energy of 720 MeV, corresponding to a Lorentz factor $\gamma = 1409$. The other two important parameters are $a_0 = 0.04$ and $\lambda_L = 515$ nm. 

## Undulator parameters
In this case, as opposed to the betatron one, we are dealing with an undulator, with strength parameter $K = a_0 = 0.04 \ll 1$, while the period $\lambda_u = \lambda_L / 2 = 0.2575\, \mu$m. Knowing the bunch charge, we can calculate $N_e = 1.6 \times 10^9$ electrons. The last parameter we are missing is the number of oscillations periods $N$, which in this case is given by the number of laser cycles per pulse, $N = \tau_L / T_0 \approx 2 \times 10^3$, with $T_0$ being the laser oscillation period $T_0 = \lambda_L / c = 1.72$ fs.

## Thomson backscattering spectrum
The scaling formulas in the undulator regime are:

$$\theta_r [\mu\text{rad}] = 10^6 \times \frac{1}{\gamma} $$
$$N_{\gamma} = 1.53 \times 10^{-2} K^2$$
$$\hbar \omega [\text{MeV}] = 2.48 \times 10^{-6} \frac{\gamma^2}{\lambda_u [\mu\text{m}] \left(1 + \frac{K^2}{2}\right)}$$

We now easily obtain $\theta_r = 700\, \mu$rad and $N_{\gamma} = 2.4 \times 10^{-5}$ photons / (electron x laser cycle). The total number of emitted photons per shot will be $N_{\gamma}^{\text{shot}} = N_{\gamma} \times N_e \times N = 2.4 \times 10^{-5} \times 1.6 \times 10^9 \times 2 \times 10^3 = 7.7 \times 10^7$ photons. Each laser pulse carries around $10^{19}$ 2.4 eV photons, of which only $1.3 \times 10^6$ will be back-scattered by each bunch to become $\gamma$ photons (arXiv:1407.3669, 2014). Finally, the fundamental radiation energy is in our case $\hbar \omega = 19.1$ MeV, versus the 19.5 MeV from the GBS specs.

## Quantum effects
The Lorentz factor for 720 MeV electrons is $\gamma = 1409$, while $K = 0.05$ and $\lambda_u = 0.2575 \, \mu$m, therefore $N_{\text{RR}} = 2 \times 10^6$, compared to $N \sim 2 \times 10^3$ cycles/pulse. The nonlinear quantum parameter $\chi_0 = 4.3 \times 10^{-4}$.

# TODO
- [ ] send to Ong together with physical explanation for $\Delta \varepsilon$ vs $Q_e$ and $\Delta \varepsilon$ versus laser depletion


- [ ] compute $r_{\beta}$ and $N$ from 15 J example by scaling and recompute all quantities that depend on them

### Radiation spectrum
- [ ] what does the betatron spectrum look like

[brilliance](https://en.wikipedia.org/wiki/Synchrotron_light_source#Brilliance):  photons/(s mrad${}^2$ mm${}^2$ 0.1% BW) vs E[keV]
spectral intensity: photons/0.1%BW vs E[keV]



[^1]: The other parameters are: $k_L = 12.2$ $\mu$m${}^{-1}$, $\omega_L = 3.65$ fs${}^{-1}$, $E_L = 2.6 \times 10^{-3}$ TV/cm and Rayleigh length $z_R = 4.7$ mm.



                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          
