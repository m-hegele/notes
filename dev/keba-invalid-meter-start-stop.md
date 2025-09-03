= Keba P30 OCPP 2.0.1: Invalid Meter Start & Stop Unit combination:

Start:
```
Aug 21 09:03:42 mira docker[2082]: INFO     v201             :322  P30_28881628: StartTransaction received from chargepoint: TransactionEventPayload(event_type='Started', timestamp='2025-08-21T07:03:33.373+0000', trigger_reason='Authorized', seq_no=0, transaction_info={'transaction_id': '28881628250821070333100549825004', 'charging_state': 'SuspendedEV'}, meter_value=[{'sampled_value': [{'value': 2114135.6, 'context': 'Transaction.Begin'}], 'timestamp': '2025-08-21T07:03:36.481+0000'}], offline=False, number_of_phases_used=None, cable_max_current=None, reservation_id=None, evse={'id': 1, 'connector_id': 1}, id_token={'id_token': '3A5AA876', 'type': 'ISO14443'}, custom_data=None)
Aug 21 09:03:42 mira docker[2082]: INFO     communicator     :231  P30_28881628: sending TransactionEventPayload to backend (event_type: Started, timestamp: 2025-08-21T07:03:33.373+0000, trigger_reason: Authorized, seq_no: 0, transaction_info: {'transaction_id': '28881628250821070333100549825004', 'charging_state': <ChargingStateType.suspended_ev: 'SuspendedEV'>, 'time_spent_charging': None, 'stopped_reason': None, 'remote_start_id': None}, meter_value: [{'timestamp': '2025-08-21T07:03:36.481+0000', 'sampled_value': [{'value': 2114135.6, 'context': <ReadingContextType.transaction_begin: 'Transaction.Begin'>, 'measurand': None, 'phase': None, 'location': None, 'signed_meter_value': None, 'unit_of_measure': None}]}], offline: False, number_of_phases_used: None, cable_max_current: None, reservation_id: None, evse: {'id': 1, 'connector_id': 1}, id_token: {'id_token': '3A5AA876', 'type': <IdTokenType.iso14443: 'ISO14443'>, 'additional_info': None}, custom_data: None) ...

```

```
TransactionEventPayload(event_type='Started', 
  timestamp='2025-08-21T07:03:33.373+0000', 
  trigger_reason='Authorized', 
  seq_no=0, 
  transaction_info={
    'transaction_id': '28881628250821070333100549825004', 
    'charging_state': 'SuspendedEV'
   }, 
   meter_value=[{'sampled_value': [
      {'value': 2114135.6, 'context': 'Transaction.Begin'}], 
    'timestamp': '2025-08-21T07:03:36.481+0000'}
  ],
  offline=False, number_of_phases_used=None, 
  cable_max_current=None, 
  reservation_id=None, 
  evse={'id': 1, 'connector_id': 1},
  id_token={'id_token': '3A5AA876', 'type': 'ISO14443'}, 
custom_data=None)
```

Start
`2114135.6` with default unit Wh = `2114.1356` kWh = `2.114` MWh

Stop: 
- differs from Start: contains `unit_of_measure`, `location`, `measurand`, but those just equal the default

`2133854.3` Wh = `2133.8543` kW = `2.133` MWh


Contained OCMF (base64 encoded):

```
OCMF|{"FV":"1.1","GI":"KEBA_KCP30","GS":"28881628","GV":"2.9.2","PG":"T125","IS":true,"IL":"TRUSTED","IF":["RFID_PLAIN","OCPP_CACHE","ISO15118_NONE","PLMN_NONE"],"IT":"ISO14443","ID":"3A5AA876","RD":[{"TM":"2025-08-21T07:03:36,000+0000 I","TX":"B","EF":"","ST":"G","RV":2114.1356,"RI":"1-b:1.8.0","RU":"kWh"},{"TM":"2025-08-21T13:34:41,000+0000 I","TX":"E","EF":"","ST":"G","RV":2133.8543,"RI":"1-b:1.8.0","RU":"kWh"}]}|{"SD":"3046022100DB36ACE4D98AD4C971C6DCAD345433C7BC9DF45F074FEBAB993AF834586D11A7022100BCFB4CDDD79295F1B5247C00F765888A9D93CAC048EB6641E497543CAB295C11"}
```
enthält `RV: 2133.8543` und `RU: kWh`

Wer macht jetzt hier den Fehler?

Stop:

```
Aug 21 15:34:50 mira docker[2082]: INFO     v201             :328  P30_28881628: StopTransaction received from chargepoint: TransactionEventPayload(event_type='Ended', timestamp='2025-08-21T13:34:41.364+0000', trigger_reason='Authorized', seq_no=1, transaction_info={'transaction_id': '28881628250821070333100549825004', 'charging_state': 'Idle', 'stopped_reason': 'EVDisconnected'}, meter_value=[
  {
    'sampled_value': [{
      'value': 2114135.6, 
      'context': 'Transaction.Begin', 
      'measurand': 'Energy.Active.Import.Register', 
      'location': 'Outlet', 
      'unit_of_measure': {'unit': 'Wh', 'multiplier': 0}
    }], '
    timestamp': '2025-08-21T07:03:36.481+0000'
  }, 

  {
    "sampled_value": [
      {
        "value": 2133854.3,
        "context": "Transaction.End",
        "measurand": "Energy.Active.Import.Register",
        "location": "Outlet",
        "unit_of_measure": {
          "unit": "Wh",
          "multiplier": 0
        }
      }
    ],
    "timestamp": "2025-08-21T13:34:41.364+0000"
  },

  {
    "sampled_value": [
      {
        "value": 2114.1356,
        "context": "Transaction.Begin",
        "signed_meter_value": {
          "signed_meter_data": "T0NNRnx7IkZWIjoiMS4xIiwiR0kiOiJLRUJBX0tDUDMwIiwiR1MiOiIyODg4MTYyOCIsIkdWIjoiMi45LjIiLCJQRyI6IlQxMjUiLCJJUyI6dHJ1ZSwiSUwiOiJUUlVTVEVEIiwiSUYiOlsiUkZJRF9QTEFJTiIsIk9DUFBfQ0FDSEUiLCJJU08xNTExOF9OT05FIiwiUExNTl9OT05FIl0sIklUIjoiSVNPMTQ0NDMiLCJJRCI6IjNBNUFBODc2IiwiUkQiOlt7IlRNIjoiMjAyNS0wOC0yMVQwNzowMzozNiwwMDArMDAwMCBJIiwiVFgiOiJCIiwiRUYiOiIiLCJTVCI6IkciLCJSViI6MjExNC4xMzU2LCJSSSI6IjEtYjoxLjguMCIsIlJVIjoia1doIn0seyJUTSI6IjIwMjUtMDgtMjFUMTM6MzQ6NDEsMDAwKzAwMDAgSSIsIlRYIjoiRSIsIkVGIjoiIiwiU1QiOiJHIiwiUlYiOjIxMzMuODU0MywiUkkiOiIxLWI6MS44LjAiLCJSVSI6ImtXaCJ9XX18eyJTRCI6IjMwNDYwMjIxMDBEQjM2QUNFNEQ5OEFENEM5NzFDNkRDQUQzNDU0MzNDN0JDOURGNDVGMDc0RkVCQUI5OTNBRjgzNDU4NkQxMUE3MDIyMTAwQkNGQjRDRERENzkyOTVGMUI1MjQ3QzAwRjc2NTg4OEE5RDkzQ0FDMDQ4RUI2NjQxRTQ5NzU0M0NBQjI5NUMxMSJ9",
          "signing_method": "ECC256",
          "encoding_method": "OCMF",
          "public_key": "eyJVSyI6IjMwNTkzMDEzMDYwNzJBODY0OENFM0QwMjAxMDYwODJBODY0OENFM0QwMzAxMDcwMzQyMDAwNDYwNkE0NDdDQUZFREZCMkQ1RUUyMTE2MDYwN0M4NEY4NEUxRjMzMjJGNkRDMTJGOEFBMjgzMzVEOEUxQTVGMkRGMzQ4NzYyQjA5QUFEQzcwNTVFM0U1MUJGQjM3RUU5MjJCRUE2NUMwNEQyNTNCNDZCRkQ5RjQ0NjlGRTA4MUQ1In0="
        }
      }
    ],
    "timestamp": "2025-08-21T07:03:36.000+0000"
  },

  {
    "sampled_value": [
      {
        "value": 2133.8543,
        "context": "Transaction.End",
        "signed_meter_value": {
          "signed_meter_data": "T0NNRnx7IkZWIjoiMS4xIiwiR0kiOiJLRUJBX0tDUDMwIiwiR1MiOiIyODg4MTYyOCIsIkdWIjoiMi45LjIiLCJQRyI6IlQxMjUiLCJJUyI6dHJ1ZSwiSUwiOiJUUlVTVEVEIiwiSUYiOlsiUkZJRF9QTEFJTiIsIk9DUFBfQ0FDSEUiLCJJU08xNTExOF9OT05FIiwiUExNTl9OT05FIl0sIklUIjoiSVNPMTQ0NDMiLCJJRCI6IjNBNUFBODc2IiwiUkQiOlt7IlRNIjoiMjAyNS0wOC0yMVQwNzowMzozNiwwMDArMDAwMCBJIiwiVFgiOiJCIiwiRUYiOiIiLCJTVCI6IkciLCJSViI6MjExNC4xMzU2LCJSSSI6IjEtYjoxLjguMCIsIlJVIjoia1doIn0seyJUTSI6IjIwMjUtMDgtMjFUMTM6MzQ6NDEsMDAwKzAwMDAgSSIsIlRYIjoiRSIsIkVGIjoiIiwiU1QiOiJHIiwiUlYiOjIxMzMuODU0MywiUkkiOiIxLWI6MS44LjAiLCJSVSI6ImtXaCJ9XX18eyJTRCI6IjMwNDYwMjIxMDBEQjM2QUNFNEQ5OEFENEM5NzFDNkRDQUQzNDU0MzNDN0JDOURGNDVGMDc0RkVCQUI5OTNBRjgzNDU4NkQxMUE3MDIyMTAwQkNGQjRDRERENzkyOTVGMUI1MjQ3QzAwRjc2NTg4OEE5RDkzQ0FDMDQ4RUI2NjQxRTQ5NzU0M0NBQjI5NUMxMSJ9",
          "signing_method": "ECC256",
          "encoding_method": "OCMF",
          "public_key": "eyJVSyI6IjMwNTkzMDEzMDYwNzJBODY0OENFM0QwMjAxMDYwODJBODY0OENFM0QwMzAxMDcwMzQyMDAwNDYwNkE0NDdDQUZFREZCMkQ1RUUyMTE2MDYwN0M4NEY4NEUxRjMzMjJGNkRDMTJGOEFBMjgzMzVEOEUxQTVGMkRGMzQ4NzYyQjA5QUFEQzcwNTVFM0U1MUJGQjM3RUU5MjJCRUE2NUMwNEQyNTNCNDZCRkQ5RjQ0NjlGRTA4MUQ1In0="
        }
      }
    ],
    "timestamp": "2025-08-21T13:34:41.000+0000"
  }
]

, offline=False, number_of_phases_used=None, cable_max_current=None, reservation_id=None, evse={"id": 1, "connector_id": 1}, id_token={"id_token": "3A5AA876", "type": "ISO14443"}, custom_data=None)


Aug 21 15:34:50 mira docker[2082]: INFO     communicator     :231  P30_28881628: sending TransactionEventPayload to backend (event_type: Ended, timestamp: 2025-08-21T13:34:41.364+0000, trigger_reason: Authorized, seq_no: 1, transaction_info: {'transaction_id': '28881628250821070333100549825004', 'charging_state': <ChargingStateType.idle: 'Idle'>, 'time_spent_charging': None, 'stopped_reason': <ReasonType.ev_disconnected: 'EVDisconnected'>, 'remote_start_id': None}, meter_value: [{'timestamp': '2025-08-21T07:03:36.481+0000', 'sampled_value': [{'value': 2114135.6, 'context': <ReadingContextType.transaction_begin: 'Transaction.Begin'>, 'measurand': <MeasurandType.energy_active_import_register: 'Energy.Active.Import.Register'>, 'phase': None, 'location': <LocationType.outlet: 'Outlet'>, 'signed_meter_value': None, 'unit_of_measure': {'unit': <UnitOfMeasureType.wh: 'Wh'>, 'multiplier': 0}}]}, {'timestamp': '2025-08-21T13:34:41.364+0000', 'sampled_value': [{'value': 2133854.3, 'context': <ReadingContextType.transaction_end: 'Transaction.End'>, 'measurand': <MeasurandType.energy_active_import_register: 'Energy.Active.Import.Register'>, 'phase': None, 'location': <LocationType.outlet: 'Outlet'>, 'signed_meter_value': None, 'unit_of_measure': {'unit': <UnitOfMeasureType.wh: 'Wh'>, 'multiplier': 0}}]}, {'timestamp': '2025-08-21T07:03:36.000+0000', 'sampled_value': [{'value': 2114.1356, 'context': <ReadingContextType.transaction_begin: 'Transaction.Begin'>, 'measurand': None, 'phase': None, 'location': None, 'signed_meter_value': {'signed_meter_data': 'T0NNRnx7IkZWIjoiMS4xIiwiR0kiOiJLRUJBX0tDUDMwIiwiR1MiOiIyODg4MTYyOCIsIkdWIjoiMi45LjIiLCJQRyI6IlQxMjUiLCJJUyI6dHJ1ZSwiSUwiOiJUUlVTVEVEIiwiSUYiOlsiUkZJRF9QTEFJTiIsIk9DUFBfQ0FDSEUiLCJJU08xNTExOF9OT05FIiwiUExNTl9OT05FIl0sIklUIjoiSVNPMTQ0NDMiLCJJRCI6IjNBNUFBODc2IiwiUkQiOlt7IlRNIjoiMjAyNS0wOC0yMVQwNzowMzozNiwwMDArMDAwMCBJIiwiVFgiOiJCIiwiRUYiOiIiLCJTVCI6IkciLCJSViI6MjExNC4xMzU2LCJSSSI6IjEtYjoxLjguMCIsIlJVIjoia1doIn0seyJUTSI6IjIwMjUtMDgtMjFUMTM6MzQ6NDEsMDAwKzAwMDAgSSIsIlRYIjoiRSIsIkVGIjoiIiwiU1QiOiJHIiwiUlYiOjIxMzMuODU0MywiUkkiOiIxLWI6MS44LjAiLCJSVSI6ImtXaCJ9XX18eyJTRCI6IjMwNDYwMjIxMDBEQjM2QUNFNEQ5OEFENEM5NzFDNkRDQUQzNDU0MzNDN0JDOURGNDVGMDc0RkVCQUI5OTNBRjgzNDU4NkQxMUE3MDIyMTAwQkNGQjRDRERENzkyOTVGMUI1MjQ3QzAwRjc2NTg4OEE5RDkzQ0FDMDQ4RUI2NjQxRTQ5NzU0M0NBQjI5NUMxMSJ9', 'signing_method': 'ECC256', 'encoding_method': 'OCMF', 'public_key': 'eyJVSyI6IjMwNTkzMDEzMDYwNzJBODY0OENFM0QwMjAxMDYwODJBODY0OENFM0QwMzAxMDcwMzQyMDAwNDYwNkE0NDdDQUZFREZCMkQ1RUUyMTE2MDYwN0M4NEY4NEUxRjMzMjJGNkRDMTJGOEFBMjgzMzVEOEUxQTVGMkRGMzQ4NzYyQjA5QUFEQzcwNTVFM0U1MUJGQjM3RUU5MjJCRUE2NUMwNEQyNTNCNDZCRkQ5RjQ0NjlGRTA4MUQ1In0='}, 'unit_of_measure': None}]}, {'timestamp': '2025-08-21T13:34:41.000+0000', 'sampled_value': [{'value': 2133.8543, 'context': <ReadingContextType.transaction_end: 'Transaction.End'>, 'measurand': None, 'phase': None, 'location': None, 'signed_meter_value': {'signed_meter_data': 'T0NNRnx7IkZWIjoiMS4xIiwiR0kiOiJLRUJBX0tDUDMwIiwiR1MiOiIyODg4MTYyOCIsIkdWIjoiMi45LjIiLCJQRyI6IlQxMjUiLCJJUyI6dHJ1ZSwiSUwiOiJUUlVTVEVEIiwiSUYiOlsiUkZJRF9QTEFJTiIsIk9DUFBfQ0FDSEUiLCJJU08xNTExOF9OT05FIiwiUExNTl9OT05FIl0sIklUIjoiSVNPMTQ0NDMiLCJJRCI6IjNBNUFBODc2IiwiUkQiOlt7IlRNIjoiMjAyNS0wOC0yMVQwNzowMzozNiwwMDArMDAwMCBJIiwiVFgiOiJCIiwiRUYiOiIiLCJTVCI6IkciLCJSViI6MjExNC4xMzU2LCJSSSI6IjEtYjoxLjguMCIsIlJVIjoia1doIn0seyJUTSI6IjIwMjUtMDgtMjFUMTM6MzQ6NDEsMDAwKzAwMDAgSSIsIlRYIjoiRSIsIkVGIjoiIiwiU1QiOiJHIiwiUlYiOjIxMzMuODU0MywiUkkiOiIxLWI6MS44LjAiLCJSVSI6ImtXaCJ9XX18eyJTRCI6IjMwNDYwMjIxMDBEQjM2QUNFNEQ5OEFENEM5NzFDNkRDQUQzNDU0MzNDN0JDOURGNDVGMDc0RkVCQUI5OTNBRjgzNDU4NkQxMUE3MDIyMTAwQkNGQjRDRERENzkyOTVGMUI1MjQ3QzAwRjc2NTg4OEE5RDkzQ0FDMDQ4RUI2NjQxRTQ5NzU0M0NBQjI5NUMxMSJ9', 'signing_method': 'ECC256', 'encoding_method': 'OCMF', 'public_key': 'eyJVSyI6IjMwNTkzMDEzMDYwNzJBODY0OENFM0QwMjAxMDYwODJBODY0OENFM0QwMzAxMDcwMzQyMDAwNDYwNkE0NDdDQUZFREZCMkQ1RUUyMTE2MDYwN0M4NEY4NEUxRjMzMjJGNkRDMTJGOEFBMjgzMzVEOEUxQTVGMkRGMzQ4NzYyQjA5QUFEQzcwNTVFM0U1MUJGQjM3RUU5MjJCRUE2NUMwNEQyNTNCNDZCRkQ5RjQ0NjlGRTA4MUQ1In0='}, 'unit_of_measure': None}]}], offline: False, number_of_phases_used: None, cable_max_current: None, reservation_id: None, evse: {'id': 1, 'connector_id': 1}, id_token: {'id_token': '3A5AA876', 'type': <IdTokenType.iso14443: 'ISO14443'>, 'additional_info': None}, custom_data: None) ...
```
