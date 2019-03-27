## Dicussion: Should we be using Vincenty distance formula over Haversine since it is supposedly "more accurate"?

TL;DR: No, not when we are primarily concerned about distances around Singapore. For distances around Singapore, one can use a corrected Haversine distance.

That is: _d<sub>corrected</sub>_ = _d<sub>Haversine</sub>_ * _r<sub>equator</sub>_ / _r<sub>average</sub>_

where _r<sub>average</sub>_ = 6371.0088km

and _r<sub>equator</sub>_ = 6378.1370km

## Explanation:

Earth is not a perfect sphere. Due to its rotation, it bulges at the equator.

![alt text](https://qph.fs.quoracdn.net/main-qimg-c5b06e986c0a082b5a41125e563262e8 "From Quora: Earth bulge")

The Vincenty formula is supposed to model the ellipsoidal shape of the earth whereas the Haversine formula assumes a uniform sphere. It is theoretically the more accurate metric.

However, implementations of Vincenty distance are _numerically unstable_ near the equator leading it to converge with the Haversine formula instead of correctly accounting for the equatorial bulge.  It is not yet clear to me whether this is due to the small delta of latitudes or the small latitude magnitudes.

See how Vincenty swings between agreeing with Haversine distance and the corrected Haversine distance in the attached notebook.
