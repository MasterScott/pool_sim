Pool Payout Simulator
=====================

Running the simulation
----------------------

    ruby test.rb

Changing the parameters
-----------------------

You can pass the following options to the run() method, or to the initializer of the simulator object:

- `:rounds`: number of rounds to run (default: 100)
- `:difficulty`: difficulty level, in mean shares per block (default: 1,500,000)
- `:miner_percent`: percentage of total hashrate owned by target miner (default: 2)
- `:average_fees`: mean amount of fees, in BTC (default: 0)
- `:withholding_percent`: percentage of pool that will withhold a found block (default: 0)
- `:hopper_percent`: percentage of base pool size that joins for the first part of the round (defualt: 0)
- `:hop_at_at`: percentage of difficulty at which hoppers jump out (default: 43.5)

Available payout models
-----------------------

- `Prop`: Straight proportional payout
- `SMPPS`: Luke-Jr's Shared-Maximum Pay-per-Share
- `XPPS`: Like SMPPS, but without debt memory

Writing your own model
----------------------

To create your own payout scheme, subclass `PoolSim` and implement the `pay_out` method.
This method should, at a minimum, update the `@honest_earnings` variable, which represents
the cumulative earnings of a single miner owning `miner_percent`% of the pool hashrate.

If you have other variables you want to plot other than the defaults (Round, Reward, Shares, and Difficulty),
you can declare them with

    class CustomPool < PoolSim
      plot :myvar1, :myvar2
    end

TODO
----

- Monte-carlo simulation
- Graphs
- Hashrate profiles
