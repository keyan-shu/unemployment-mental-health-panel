# pydynpd compatibility substitutions
Upstream: https://github.com/dazhwu/pydynpd ; version 0.2.2.
panel_data.py: np.in1d -> np.isin for one-dimensional membership.
specification_tests.py: explicit .item() for 1x1 Hansen and AR statistic arrays.
No equation, moment condition, lag rule or covariance formula was changed.
The included license applies to the vendored source.
