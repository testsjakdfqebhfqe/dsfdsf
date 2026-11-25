---
excerpt: >-
  This endpoint is used to send odds data for a particular sport event,
  identified by its unique id.

  The same endpoint is used for **PRE_MATCH**, **LIVE**, and
  **COMPETITION_ODDS** messages.


  ## Important Information


  ### 1) PRE_MATCH vs LIVE vs COMPETITION_ODDS

  You send PRE_MATCH, LIVE, and COMPETITION_ODDS through this endpoint, but you
  must select the correct **product** in the URL and the correct **producer** in
  the message.

  | Phase | `{product}` in URL | `producer` in message |

  |---|---|---|

  | Pre-match odds | `pre` | `PRE_MATCH` |

  | Live odds | `liveodds` | `LIVE` |

  | Competition odds | `codds` | `COMPETITION_ODDS` |


  #### PRE_MATCH cut-off rule ~~(15 minutes)~~

  ~~We enforce a strict 15-minute window right before the sport event start time
  that separates PRE_MATCH from LIVE updates:~~  

  ~~- `PRE_MATCH` messages are accepted **until 15 minutes before** the sport
  event start time.~~  

  ~~- `LIVE` messages are accepted **15 minutes before** the sport event start
  time onward.~~  

  | 🚧 DEPRECATED 🚧 |

  | --- |

  | We're in the process of switching to cut-off of 0, i.e. at the scheduled
  start time.<br/>For more details please see the new pre-match section. |


  #### What happens if you send the wrong type at the wrong time?

  Messages outside the allowed window are **not processed** and you will receive
  a `validation_failure` callback.


  #### Sport event state expectations

  Your payload includes `betting_event_state`. This state should reflect the
  sport event phase:

  - In `PRE_MATCH`, `sport_event_status` is typically `NOT_STARTED`. Period
  details (e.g. `period` / `periods`) are omitted.

  - In `LIVE`, `sport_event_status` is typically `IN_PROGRESS`. Period and clock
  details are present.


  ### 2) Rate limit and batching

  We expect **maximum 1 message per second per sport event** from you

  If your system is able to generate more than 1 odds update within 1 second,
  **then you need to collate those updates and send as 1 single message each
  second**


  ### 3) Message payload conventions 

  -   We expect to receive  **true odds**  with no margins applied. Our clients
  have the flexibility to configure their own odds keys (margin) to suit their
  respective risk profiles.

  -   A message  **without  `markets`**  means that some other information has
  changed (e.g.  `sport_event_status`), while markets have not.

  -   When market has inactive outcome,  **do not send**  the  `odds`  field for
  that outcome.

  -   Avoid sending odds with values near to  `1.01`, as for some bookmakers
  such updates may be ignored. Moreover, some outcomes or markets can be
  automatically deactivated!

  -   Use  `Sportradar's Market Lifecycle`  section to find the description of
  each market status. We expect you to align with our market's definition and
  status.


  **You can find examples of such messages in the  `examples`  tab. Please find
  the corresponding example to your sport and markets and apply mappings
  similarly.** 
api:
  file: base (1).json
  operationId: post_product-partner-id-sport-event-id-odds
hidden: false
---