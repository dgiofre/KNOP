# KNOP

## Kinetic monte carlo code driven by a Neural netwOrk Potential
  
  Implementation of this scheme was achieved by incorporating the KMC algoritm into i-Pi, 
  which is a universal force engine interface code written in Python, designed to be used 
  together with an ab-initio, force-field, or Neural Network potential evaluation of the 
  interactions between the atoms.
 
## KNOP is a specific engine of i-Pi software
  kinetic MC simulation algorithm carries out elementary swaps on a virtual 3D grid with 
  Periodic Boundery Condiction applied. 
  This grid is on-lattice and  follows the fcc-sites (example for Al). It can represent an 
  idealized picture of vacancy migrations and precipitation sequence for fcc-alloy with 
  many trace elements (example for two trace elements, i.e. Silicon and Magnesium). 
  The defects as solute atoms and vacancies, are artificially and randomly introduced into 
  the system to represent an initial state that corresponds to a Supersaturated Solid Solution.
  
  Next, the energy of local minima is calculated for all these tracked-down process. 
  The energy minimization cycle is performed by a fixed number of steps of the Limited memory BFGS. 

### kMC Rates

   The rates are, in turn, estimated based on activation barriers, which are a correction to those 
   calculated with the NEB method for the vacancy-assisted jump of an isolated solute atom. 
   The new activation barrier for a swap involving a solute $X$ is given by
   
  ````
  E_{X,i}=\frac{(E^{NN}_{i,LMS}(n+1)-E^{NN}_{LMS}(n))}{2}+E_X^{DFT}
  ````
  
  where $E^{NN}_{LMS}(n) $ is the local minimized Neural Network energy at KMC 
  step $n$ and $E^{NN}_{i,LMS}(n+1)$ 
  is the minimized NN energies for the $i$-th candidate at step $n+1$.  
  $E_X^{DFT}$ is the DFT energy barrier for a swap of an isolate atom (e.g Vacancy/Al-atom, 
  Vacancy/Mg-atom, or Vacancy/Si-atom).
  Rates computed based on these barriers are consistent with detailed balance.

## i-PI
 
  A Python interface for ab initio path integral molecular dynamics simulations.
  i-PI is composed of a Python server (i-pi itself, that does not need to be
  compiled but only requires a relatively recent version of Python and Numpy)
  that propagates the (path integral) dynamics of the nuclei, and of an external
  code that acts as a client and computes the electronic energy and forces.
  
  This is typically a patched version of an electronic structure code, but a
  simple self-contained Fortran driver that implements Lennard-Jones and
  Silvera-Goldman potentials is included for test purposes.
 
  http://ipi-code.org/   
  
  See [README.rst](README.rst)]
  
  [Ceriotti, More, Manolopoulos, Comp. Phys. Comm. 185, 1019-1026 (2014)](https://www.sciencedirect.com/science/article/pii/S001046551300372X?via%3Dihub)

## License

This project, as i-Pi software, is under the MIT/GPLv3 License.
