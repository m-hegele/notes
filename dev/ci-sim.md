# Run simulation in CI

broken:
- [ ] full_ev: constantly in prepare-charging:

boring scenarios:
- mini
- kona_cv_cont
- perfect3_cv_10A
- perfect3_cv_cont
- rcur_sym_opt: even with sym
- vw_egolf_cv_8A
- vw_id3_cv_5A

vehicle not full at the end:
- sus_ev_problem

interesting:
- dynamic_capacity_groups
- full_ev
- interpolation_challenge
- nightly_sleep
- nissan_leaf
- nissan_leaf_with_perfect
- non_monotonous
- non_monotonous_zero
- perfect_with_lag
- rauma
- seq_charging
- seq_charging_rand
- sequential
- sequential_three
- sequential_three_enough_for_two
- simple_dyn_limit
- simulated_grid_connection_point
- sus_ev_problem
- two_cars_one_with_long_delay
- uncontrollable_load
- unequal_num_cps
