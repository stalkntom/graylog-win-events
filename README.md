# graylog-win-events
Two Graylog Pipeline rules for filtering Windows Eventlogs by the EventID field. The first method is done through defining a list of EventIDs to route to another stream (Allow list). The second method is defining the EventIDs that should not be routed to another stream (Drop list). Prior to these two routing rules another is used to override the SourceModuleName to match SIEM Parser requirements.

1) Events are ingested into the win_event_all Stream
2) Two Pipelines run:
- _win_event_allow_ 
- _win_event_drop_  
Both pipelines run the _set_source_module_name_ rule at stage 0. Other pipeline rules can be included here.
3) The _win_event_allow_ pipeline stage 1 rule _win_event_allow_list_ defines the EventIDs that should be routed to the _win_event_allowed_ Stream
4) The _win_event_drop_ pipeline stage 1 rule _win_event_drop_list_ defines the EventIDs that should not be routed to the _win_event_dropped_ Stream

3 Streams:
- _win_event_all_ - Windows Events from "gelf_tcp" Input
- _win_event_allowed_ - Windows Events allowed from _win_event_allow_list_ Pipeline rule
- _win_event_dropped_ - Windows Events not dropped from _win_event_drop_list_ Pipeline rule  
<img width="847" alt="image" src="https://user-images.githubusercontent.com/4864411/169683647-3133ff7c-fa52-4802-9416-4afc4d94e7f4.png">

_win_event_all_ Stream Rule:  
<img width="292" alt="image" src="https://user-images.githubusercontent.com/4864411/169683727-c80b21ac-5fd3-46b0-9f93-33668b1d1f17.png">

2 Pipelines:  
<img width="376" alt="image" src="https://user-images.githubusercontent.com/4864411/169683743-f289a42e-da84-418b-9a02-883dadb9e3b3.png">

3 Pipeline rules:  
<img width="355" alt="image" src="https://user-images.githubusercontent.com/4864411/169684197-c10819cd-d418-47f9-ac8f-ca2ac10dee75.png">

Pipeline _win_event_allow_:  
<img width="843" alt="image" src="https://user-images.githubusercontent.com/4864411/169684223-9daf4c0f-9760-4afc-9a0e-d81cd069a01d.png">

Pipeline _win_event_drop_:  
<img width="842" alt="image" src="https://user-images.githubusercontent.com/4864411/169684242-e7ebbc3c-ace8-4336-9b33-86e6e9db444e.png">
