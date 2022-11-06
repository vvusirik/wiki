# Finance
**Filtration** - tells us what knowledge we have at a given time. If a process is F(T)-measurable, then at any time t <= T, the realizations f this process are known.
Ex. We know the historical stock values for a stock today exactly, but we don't know the future values.
A process is "adapted" to a filtration if it does not rely on information beyond the filtration.
* Adapted example for F(t) - W(t) where W(t) is a Weiner process. Or W^2(t) - t
* Non-Adapted example for F(t) - W(t + 1) where W is a Weiner process

**Conditional Expectations** - E[X | G] = E[E[X | F] | G] where X is a random variable, G and F are filtrations such that G <= F (G contains F)
