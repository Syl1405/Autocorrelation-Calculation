# Autocorrelation-Calculation

Autocorrelation is the correlation of a signal with a delayed copy of itself as a function of delay. Informally, it is the similarity between observations as a function of the time lag between them.

By reading a signal file(file ends with `.bin` or `.txt`), the pgogram will calculate things like

```
Sums[0] = A[0]*A[0] + A[1]*A[1] + ... + A[NUMELEMENTS-1]*A[NUMELEMENTS-1]
```

It will give us a large number, and we need to shift the array over one index and do the pairwise multiplication again. 
if the signal is truly noisy, there will be positive and negative array values, giving both positive and negative products. By doing this shift before multiplying, we will get a much smaller sum.

In the nutshell, the program is doing things like but using MPI parallelism:
```
Sums[0] = A[0]*A[0] + A[1]*A[1] + ... + A[NUMELEMENTS-2]*A[NUMELEMENTS-2] + A[NUMELEMENTS-1]*A[NUMELEMENTS-1]
Sums[1] = A[0]*A[1] + A[1]*A[2] + ... + A[NUMELEMENTS-2]*A[NUMELEMENTS-1] + A[NUMELEMENTS-1]*A[NUMELEMENTS]
Sums[2] = A[0]*A[2] + A[1]*A[3] + ... + A[NUMELEMENTS-2]*A[NUMELEMENTS]   + A[NUMELEMENTS-1]*A[NUMELEMENTS+1]
```

This project is to compare the performances across different numbers of processors after using MPI.
