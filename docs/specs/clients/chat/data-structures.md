# Data Structures

In this document we define data structures and definitions used in the chat api

## Invite

`Invite` is a structure that is returned by SDK. Is extracted from Invite Proposals did-jwt claims. To get author account identity must be resolved from `iss` field. A map of type `Map<number, Invite>` is returned on `getReceivedInvites(params: {account: string})`. Topic is the key of the map.


```jsonc
{
  "id": number,
  "message": string, // character limit is 200. Must be checked by SDK before sending
  "inviterAccount": string,
  "inviteeAccount": string,
  "inviterPublicKey": string,
}
```

## Media

`Media` is an optional parameter used in Message to append a media file reference sent together with the plaintext message.

```jsonc
{
  "type": string,
  "data": string, // character limit is 500. Must be checked by SDK before sending
}
```

## Message

`Message` is an structure that is returned by SDK. Is extracted from Chat Message did-jwt claims. To get author account identity must be resolved from `iss` field. An array of `Messages` is returned on `getMessages(params: {topic: string;})`

```jsonc
{
  "topic": string,
  "message" : string, // character limit is 1000. Must be checked by SDK before sending
  "authorAccount": string, // to distinguish who sent it
  "timestamp": Int64,
  "media": Media // optional
}
```

## SentInvite

`SentInvite` structure keeps track of state of sent Invites. If Invite is approved by peer it should be removed from storage, if rejected should stay in storage. An array of `SentInvite` is returned on `getSentInvites(params: {account: string})`
```jsonc
{
  "id": number,
  "message": string, // character limit is 200
  "inviterAccount": string,
  "inviteeAccount": string,
  "status": 'pending' | 'rejected'
}
```

## Thread

A map of type `Map<string, Thread>` is returned on `getThreads(params: {account: string})`. Topic is the key of the map.

```jsonc
{
  "topic": string,
  "selfAccount": string,
  "peerAccount": string
}
```
