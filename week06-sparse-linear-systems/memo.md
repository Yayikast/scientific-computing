# Memo: can similar restaurants and the street-load model ship?

Yes, both features are feasible: they run on an ordinary 16 GB laptop, as long as we only store the numbers that aren't zero.

**The Problem**: 
The review table has 40,000 reviews and 120,000 word pieces. Most cells are zero, because each review only uses a few words. If we store every cell, zeros included, the table needs 38.4 GB. A 16 GB laptop can't hold that, so the program crashes before it starts.

**The Fix**: 
Store only cells that have values. On a smaller test table with 6,000 reviews, just 0.4% of cells were filled. Storing everything took 384 MB, but sparse storage took only 2.33 MB, about 165 times less. At full size that's roughly 230 MB, which fits easily.

**Speed**: 
Skipping the zeros also makes things faster. Finding similar reviews was about 64 times faster. Solving the street model took about 16 ms instead of 656 ms, around 42 times faster. Both ways gave the same answer.

**Which Solver**: 
Jacobi and Gauss-Seidel improve a guess round by round and needed 71 and 39 rounds. They work, but they stop at a set accuracy, while spsolve gets the answer in one go to full precision and still fits in memory at full city size, so that's the one I would ship.

**Hardware**: 
Everything ran on my Microsoft Surface Pro 9 (Intel i7, 16 GB RAM). For a city with 300,000 intersections, the sparse street model needs about 20 MB to store and under half a GB to solve. Storing everything would need about 720 GB, which no laptop has.

**Limits**: 
I used generated test data at a smaller size, and timings change from run to run. The ratios matter more than the exact times.

**Next Step**: 
Build both features with sparse storage, use spsolve for the city, and test again on real data.

**Real-World Link**: 
scikit-learn's TfidfVectorizer, a common tool that turns reviews into numbers, also gives back a sparse matrix, for the same reason my table shows: text is mostly zeros, so sparse storage takes 2.33 MB instead of 384 MB.