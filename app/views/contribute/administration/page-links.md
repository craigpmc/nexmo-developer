---
title: Page Links
---

# Page Link Reporting

Nexmo Developer supports some reporting `rake` commands for showing links in to, and out from pages. This helps us visualise where our heavily linked pages are, and which pages we need to link to more. You can output the data as a table, plain text or as a Graphviz digraph.

This information can be used to improve cross-linking between pages, or identify content that is isolated and potentially unused

## Usage

> [partial_url] can be any string e.g. /voice/voice-api and only
matching source URLs will be returned. (`from` for _outbound and `to`
for _inbound)

* `rake links:report_outbound [partial_url]` - Generate a table containing
a list of pages, and all pages that they link to

* `rake links:report_inbound [partial_url]` - Generate a table containing
a list of pages, and all pages that link to it

* `rake links:no_links_outbound` - Show all pages with no outbound links

* `rake links:no_links_inbound` - Show all pages with no inbound links

* `rake links:graph_outbound [partial_url]` - Generate a Graphviz Digraph
containing all pages that match [partial_url]

* `rake links:graph_inbound [partial_url]` - Generate a Graphviz Digraph
containing all pages that link to [partial_url]


### Examples 

#### Outbound links from urls containing `/voice/voice-api/guides`

```
$ bundle exec rake links:report_outbound /voice/voice-api/guides

+--------------------------------------------+--------------------------------------------------------------------+
| From                                       | To                                                                 |
+--------------------------------------------+--------------------------------------------------------------------+
| /voice/voice-api/guides/legs-conversations | /voice/voice-api/guides/endpoints                                  |
+--------------------------------------------+--------------------------------------------------------------------+
| /voice/voice-api/guides/ncco               | /voice/voice-api/ncco-reference#record                             |
|                                            | /voice/voice-api/ncco-reference#conversation                       |
|                                            | /voice/voice-api/ncco-reference#connect                            |
|                                            | /voice/voice-api/ncco-reference#talk                               |
|                                            | /voice/voice-api/ncco-reference#stream                             |
|                                            | /voice/voice-api/ncco-reference#input                              |
+--------------------------------------------+--------------------------------------------------------------------+
| /voice/voice-api/guides/lex-connector      | /voice/voice-api/guides/websockets                                 |
|                                            | /voice/voice-api/guides/text-to-speech#voice-names                 |
+--------------------------------------------+--------------------------------------------------------------------+
| /voice/voice-api/guides/troubleshooting    |                                                                    |
+--------------------------------------------+--------------------------------------------------------------------+
| /voice/voice-api/guides/endpoints          |                                                                    |
+--------------------------------------------+--------------------------------------------------------------------+
| /voice/voice-api/guides/dtmf               | /voice/voice-api/ncco-reference#input                              |
|                                            | /api/voice#createCall                                              |
+--------------------------------------------+--------------------------------------------------------------------+
| /voice/voice-api/guides/call-flow          | /voice/voice-api/ncco-reference                                    |
|                                            | /voice/voice-api/webhook-reference#event-webhook                   |
|                                            | /concepts/guides/webhooks                                          |
|                                            | /voice/voice-api/guides/legs-conversations                         |
|                                            | /voice/voice-api/webhook-reference                                 |
+--------------------------------------------+--------------------------------------------------------------------+
| /voice/voice-api/guides/recording          | /voice/voice-api/ncco-reference#conversation                       |
|                                            | /voice/voice-api/ncco-reference#record                             |
+--------------------------------------------+--------------------------------------------------------------------+
| /voice/voice-api/guides/text-to-speech     | /api/voice#startTalk                                               |
|                                            | /voice/voice-api/ncco-reference                                    |
+--------------------------------------------+--------------------------------------------------------------------+
| /voice/voice-api/guides/numbers            |                                                                    |
+--------------------------------------------+--------------------------------------------------------------------+
| /voice/voice-api/guides/websockets         | /voice/voice-api/guides/ncco                                       |
|                                            | /voice/voice-api/guides/call-flow#answer-url-payload               |
|                                            | /voice/voice-api/building-blocks/play-an-audio-stream-into-a-call/ |
+--------------------------------------------+--------------------------------------------------------------------+
+--------------------------------------------+--------------------------------------------------------------------+

```

#### No outbound links from these pages
```
$ bundle exec rake links:no_links_outbound

/messages/external-accounts/api-reference
/messages/tutorials
/messages/concepts/facebook
/messages/concepts/viber
/messages/concepts/whatsapp
/messages/api-reference
/messages/building-blocks/client-library
/messages/building-blocks/create-an-application
/messages/building-blocks/install-cli
/verify/tutorials
/verify/api-reference
/dispatch/external-accounts/api-reference
/dispatch/tutorials
/dispatch/concepts/workflows
/dispatch/api-reference
/dispatch/building-blocks/client-library
/dispatch/building-blocks/create-an-application
/dispatch/building-blocks/install-cli
/redact/api-reference
/redact/building-blocks/redact-using-id
/audit/tutorials
/audit/api-reference
/voice/sip/configure/freeswitch
/voice/sip/configure/asterisk
/voice/sip/configure/freepbx
/voice/voice-api/tutorials
/voice/voice-api/guides/troubleshooting
/voice/voice-api/guides/endpoints
/voice/voice-api/guides/numbers
/voice/voice-api/api-reference
/voice/voice-api/building-blocks/mute-a-call
/voice/voice-api/building-blocks/play-text-to-speech-into-a-call
/voice/voice-api/building-blocks/retrieve-info-for-a-call
/voice/voice-api/building-blocks/earmuff-a-call
/voice/voice-api/building-blocks/play-dtmf-into-a-call
/voice/voice-api/building-blocks/play-an-audio-stream-into-a-call
/voice/voice-api/building-blocks/transfer-a-call
/voice/voice-api/building-blocks/retrieve-info-for-all-calls
/stitch/concepts/mos
/stitch/concepts/jwt-acl
/stitch/in-app-voice/call-statuses
/stitch/api-reference
/concepts/guides/oauth
/account/secret-management/api-reference
/account/secret-management/building-blocks/list-all-secrets
/account/secret-management/building-blocks/revoke-a-secret
/account/secret-management/building-blocks/create-a-secret
/account/secret-management/building-blocks/fetch-a-secret
/messaging/sns/building-blocks/subscribe-a-user
/messaging/sns/building-blocks/sending-a-message
/messaging/sms/tutorials
/messaging/sms/guides/SMPP-access
/messaging/sms/api-reference
/number-insight/tutorials
/number-insight/guides/cnam
/number-insight/api-reference
/conversation/tutorials
/conversation/concepts/event
/conversation/concepts/user
/conversation/cli-reference
/conversation/api-reference
/conversation/building-blocks/member/get-member
/conversation/building-blocks/member/create-member
/conversation/building-blocks/member/update-member
/conversation/building-blocks/member/list-members
/conversation/building-blocks/member/delete-member
/conversation/building-blocks/user/update-user
/conversation/building-blocks/user/delete-user
/conversation/building-blocks/user/get-user
/conversation/building-blocks/user/list-user-conversations
/conversation/building-blocks/user/list-users
/conversation/building-blocks/user/create-user
/conversation/building-blocks/leg/delete-leg
/conversation/building-blocks/leg/list-legs
/conversation/building-blocks/event/get-event
/conversation/building-blocks/event/create-event
/conversation/building-blocks/event/list-events
/conversation/building-blocks/event/delete-event
/conversation/building-blocks/conversation/list-conversations
/conversation/building-blocks/conversation/update-conversation
/conversation/building-blocks/conversation/get-conversation
/conversation/building-blocks/conversation/delete-conversation

```

### Render Graphviz digraphs

This example will render a digraph containing all outbound links from `/voice/voice-api/guides` as a file named `voice-graph.png`

```
bundle exec rake links:graph_outbound /voice/voice-api/guides > voice-graph
dot -Tpng voice-graph > voice-graph.png
```

