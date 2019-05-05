

# Caracterizarea radiatiei provenita din PWFAs (plasma wakefield accelerators)

## Prezentarea pe scurt proiectului, cu menționarea țintelor propuse a fi atinse prin implementarea proiectului

Conceptul unui accelerator de electroni bazat pe interactiunea laser-plasma (accelerare wakefield) provine din articolul lui Tajima si Dawson din 1979  [^1]. Intre timp, acest domeniu a devenit unul international ce cuprinde experimente, modelare teoretica si simulari numerice din ce in ce mai complexe [^2]. In ultimii ani doua grupuri experimentale au demonstrat accelerarea de tip "wakefield" cu ajutorul laserilor (LWFA), capturand electroni din plasma, care sunt apoi accelerati cu ajutorul laserului pana la o energie de 2-4 GeV si o sarcina totala de ordinul nano-Coulombilor intr-o distanta de cativa centimetri (Wang et al., 2013; Leemans et al., 2014). Atingerea acestor energii pe o distanta scurta (comparata cu km in cazul acceleratoarelor traditionale bazate pe radio-frecventa) este posibila datorita campurilor electrice din interiorul plasmei. In timp ca acceleratoarele clasice sunt limitate la un camp electric de MV/cm datorita limitei structurilor metalice, in interiorul unui accelerator bazat pe plasma se pot atinge campuri de ordinul GV/cm.
Numeroase laboratoare au convertit acceleratoarele LWFA in surse de raze X bazate pe emisia betatron a electronilor accelerati, radiatie de tip sincrotron in undulatori externi sau radiatie de tip Thomson prin backscattering [^3]. Acceleratoare LWFA cu doua stagii au fost deja dezvoltate [^4] si reprezinta un pas important in directia cresterii energiei per particula. 
In timp ce intr-un LWFA fascicolul laser este cel care isi transfera energia plasmei, accelerand electronii, exista si optiunea de o folosi particule incarcate precum electroni sau pozitroni in locul laserului [^5]. Aceste "bunch"-uri de particule relativiste pot captura electroni in interiorul plasmei, accelerandu-i prin wakefield-ul creat - de unde denumirea de plasma wakefield acceleator (PWFA). Rolul fortei ponderomotoare care genereaza wakefield-ul este acum preluat de forta Coulomb a bunch-ului, iar transitia intre regimula PWFA linear si neliniar are loc atunci cand densitatea bunch-ului este aproximativ egala cu densitatea plasmei prin care acesta de propaga. In acest proiect regimul neliniar de tip "blow out" este de interes, datorita similitudinii sale cu regimul "bubble" din cadrul LWFAs. 

## Scopul cercetarii
Obiectul acestui proiect il constituie studiul radiatiei emise de electronii injectati in interiourl zonei "blow out" din PWFAs. Acesti electroni au o miscare oscilatorie datorita campului electric radial, si drept urmare emit radiatie de tip "sincrotron". Spre deosebire de LWFA insa, acceleratoarele de tip PWFA nu prezinta defazarea electronilor fata de bunch-ul care ii accelereaza. Lipsa acestei defazari permite optimizarea radiatiei emise de acesti electroni, atat in ce priveste energia fotonilor emisi, cat si numarul fotonilor. Pentru caracterizarea si optimizarea radiatiei provenita dintr-un PWFA vor fi necesare numeroase simulari numerice de tip "particle in cell" folosind codul PIConGPU [^6], interpretarea rezultatelor obtinute in urma simularilor cat si dezoltarea de modele semi-analitice.

## Obiective
- familiarizarea cu rularea si modificarea codului PIConGPU
- dezvoltarea unei noi metode de injectare a bunch-urilor de electroni in locul laserului intr-o simulare "particle in cell"
- modelarea radiatiei emise de electroni folosind formalismul Liénard–Wiechert [^7]
- caracterizarea si optimizarea raditiei emise de catre electronii accelerati in PWFA

## Rezultate estimate
-   Diseminarea rezultatelor prin seminarii si conferinte internationale
-   Trimiterea spre publicare intr-un jurnal de specialitate a unui articol in care se prezinta metoda nou dezvoltata


### Bibliografie
[^1]: Tajima, Toshiki, and John M. Dawson. "Laser electron accelerator." Physical Review Letters 43.4 (1979): 267
[^2]: Esarey, Eric, C. B. Schroeder, and W. P. Leemans. "Physics of laser-driven plasma-based electron accelerators." Reviews of modern physics 81.3 (2009): 1229
[^3]: Corde, Sébastien, et al. "Femtosecond x rays from laser-plasma accelerators." Reviews of Modern Physics 85.1 (2013): 1
[^4]: Kim, Hyung Taek, et al. "Enhancement of electron energy to the multi-GeV regime by a dual-stage laser-wakefield accelerator pumped by petawatt laser pulses." Physical review letters 111.16 (2013): 165002
[^5]: Chen, Pisin, et al. "Acceleration of electrons by the interaction of a bunched electron beam with a plasma." Physical review letters 54.7 (1985): 693
[^6]: Bussmann, Michael, et al. "Radiative signature of the relativistic Kelvin-Helmholtz Instability."  High Performance Computing, Networking, Storage and Analysis (SC), 2013 International Conference for. IEEE, 2013.
[^7]: Jackson, John David. Classical electrodynamics. John Wiley & Sons, 2012.