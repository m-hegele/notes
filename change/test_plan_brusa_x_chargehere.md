# Test Plan: Brusa AWC x ChargeControl

. Vehicle arrives
  - Status changes to Occupied -> OCPPProxy state = Preparing


* StatusNotification
* TransactionStarted
* TransactionStopped
* TransactionUpdated (ChargingState)
* TransactionUpdated (MeterValue)
* (Authorize)
* SetChargingProfile
* 
