
# Matrix Calendar MSC

When taking a look at common calendar solutions
used at home or at organizations the "Outlook" calendar comes quickly to mind.

Invitations are sent to mailboxes and the RSVPs are being sent back.

*Note: The term "calendar item" is being used over the term "event"
to avoid conflicts with the timeline events.
The term "event" must only be used to refer to such.*

## Proposal

### The calendar item

People may send `msc.c0ffeecode.calendar.item` events to a room
to invite all of the room members to that calendar item.

The scheme of that event's content are described in a [JSON schema](./msc-cal-item-scheme.json).

It may be altered using the `m.replace` relation type.

The properties found in the item scheme are itended to align to
[JSCalendar (RFC8984)](https://datatracker.ietf.org/doc/rfc8984/) where appropriate.

### Calendar responses

For responding to invitations of `msc.c0ffeecode.calendar.item` events,
clients must respond in a `m.thread` relation to that event.

The scheme of a calendar response event can be found [here](./msc-cal-response-scheme.json)

Those responses may be of the type `msc.c0ffeecode.calendar.response`,
which may be altered in a relation.

The `agreed_time` property must be set to the exact same values
as the version of the calendar item agreed on.
A response event whose `agreed_time` properties do
differentiate from the latest calendar item version
are to be treated as outdated and hence invalid.
Hence, if the time of an calendar item is changed back to previous time,
replies accepting that previous time are valid again.

When a user accepted a calendar item and then agrees to changed version,
its previous versions must be treated as invalid regardless of their content.

<!-- // TODO: Change or remove -->
*Possible consideration: If the new time span is in between of the
time span agreed on, it may be considerable to continue treating it as valid.*

### A personal room

For personal calendar items, it may be advisable to create a personal room.
That room's ID can be be noted in the user's account data
with a type of `msc.c0ffeecode.prefered_private_room` to find it more easy so
clients can advertise creating items in that room for such purpose.

That entry may contain an object with a key `room_id`
whose value must be the internal room ID as a string.

## Potential issues

This does not address:

- Permissions for creating calendar items
- Reaccurances
- Room and resource management
- Matrix-external invitations (e.g. via email)
- Forwarding invitations, cross-room invitations

Also, the term "calendar item" does not sound very nice
and may be considered to be changed.

## Alternatives

- Mapping to iCal
- Mapping to JSCalendar

There is/was [another proposal](https://github.com/matrix-org/matrix-spec/issues/284) on this subject,
but it is unavailable thanks to Google Docs.

## Security considerations

## Unstable prefix

Since this is an MSC,
this proposal uses `msc.c0ffeecode.` instead of `m.`.

The following tags are defined:

- `msc.c0ffeecode.calendar.item`
- `msc.c0ffeecode.calendar.invitation_reply`
- `msc.c0ffeecode.prefered_private_room`

## Dependencies
