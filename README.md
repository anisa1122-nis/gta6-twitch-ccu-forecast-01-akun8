# GTA VI Twitch CCU forecast — akun 8 (anisa1122-nis / golden-lynx-91)

Competition: gta6-twitch-ccu-forecast-01. Forecast Twitch concurrent viewers in
the Grand Theft Auto VI category, hours 2-24 of release day (2026-11-19 UTC),
as five quantiles per hour.

Model: per-hour weighted OLS log regression on rolling-midnight comparables,
recency-weighted. For each hour h, fit log(viewers_h) = a_h + b_h *
log(viewers_1) by weighted least squares, each launch weighted by its release
year (0.5 for 2018, rising 0.125/year to 1.5 for 2026); predict at GTA VI's
hour-1 print; spread = residual std, clamped to [0.20, 1.00]. Quantiles:
q_tau(h) = exp(pred_h + z_tau * s_h).

Leave-one-out backtest over the 12 rolling comparables: pinball loss 0.253 vs
the house baseline's 0.357 (29% better), winning 10 of 12 cases.

Run: `MAKEFUN_INPUT_DIR=input MAKEFUN_OUTPUT_DIR=out python3 main.py`
