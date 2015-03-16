---
layout: post
title: PHPMailer add event to Outlook calendar
category: code
tags:
- code
- PHP
- PHP Mailer
- outlook
- calendar
- event
---

A quick guide to getting PHPMailer send proper 
Outlook events. I'd like to highlight three significant variables in the code i.e. $event_id, $sequence, $status.

```php
$event_id = 1234;
```

This is used to generate a UID for this particular event and applys when making future alterations to an event.

```php
$sequence = 0;
```

The sequence marks different 'revisions' of the event as significant changes are made. Ideally starts from zero. If e.g. the date is changed, the second email sent will have 1 as the sequence number. This parameter together with the UID helps Outlook update the correct event on the user's calendar.

```php
$status = 'TENTATIVE';
```

Status parameter can only have values 'TENTATIVE', 'CONFIRMED' or 'CANCELLED'. Probably used in that order as well. When set to cancelled, the emailed event update will mark the event as cancelled by the organizer and also prompt the user to remove it from their calendar.

```php
// event params
$summary = 'Summary of the event';
$venue = 'Simbawanga';
$start = '20140820';
$start_time = '160630';
$end = '20140820';
$end_time = '180630';

//PHPMailer
$mail = new PHPMailer();
$mail->isSMTP();
$mail->SMTPDebug = 0;
$mail->Host = 'kaserver.com';
$mail->Port = 25;
$mail->SMTPAuth = false;
$mail->IsHTML(false);
$mail->setFrom('your@kaserver.com', 'Water Lemon');
$mail->addReplyTo('your@kaserver.com', 'Water Melon');
$mail->addAddress('them@kaserver.com','Recipient Addy');
$mail->ContentType = 'text/calendar';

$mail->Subject = "Outlooked Event";
$mail->addCustomHeader('MIME-version',"1.0");
$mail->addCustomHeader('Content-type',"text/calendar; method=REQUEST; charset=UTF-8");
$mail->addCustomHeader('Content-Transfer-Encoding',"7bit");
$mail->addCustomHeader('X-Mailer',"Microsoft Office Outlook 12.0");
$mail->addCustomHeader("Content-class: urn:content-classes:calendarmessage");

$ical = "BEGIN:VCALENDAR\r\n";
$ical .= "VERSION:2.0\r\n";
$ical .= "PRODID:-//YourCassavaLtd//EateriesDept//EN\r\n";
$ical .= "METHOD:REQUEST\r\n";
$ical .= "BEGIN:VEVENT\r\n";
$ical .= "ORGANIZER;SENT-BY=\"MAILTO:organizer@kaserver.com\":MAILTO:onbehalfoforganizer@kaserver.com\r\n";
$ical .= "ATTENDEE;CN=them@kaserver.com;ROLE=REQ-PARTICIPANT;PARTSTAT=ACCEPTED;RSVP=TRUE:mailto:organizer@kaserver.com\r\n";
$ical .= "UID:".strtoupper(md5($event_id))."-kaserver.com\r\n";
$ical .= "SEQUENCE:".$sequence."\r\n";
$ical .= "STATUS:".$status."\r\n";
$ical .= "DTSTAMPTZID=Africa/Nairobi:".date('Ymd').'T'.date('His')."\r\n";
$ical .= "DTSTART:".$start."T".$start_time."\r\n";
$ical .= "DTEND:".$end."T".$end_time."\r\n";
$ical .= "LOCATION:".$venue."\r\n";
$ical .= "SUMMARY:".$summary."\r\n";
$ical .= "DESCRIPTION:".$event['description']."\r\n";
$ical .= "BEGIN:VALARM\r\n";
$ical .= "TRIGGER:-PT15M\r\n";
$ical .= "ACTION:DISPLAY\r\n";
$ical .= "DESCRIPTION:Reminder\r\n";
$ical .= "END:VALARM\r\n";
$ical .= "END:VEVENT\r\n";
$ical .= "END:VCALENDAR\r\n";

$mail->Body = $ical;

//send the message, check for errors
if(!$mail->send()) {
$this->error = "Mailer Error: " . $mail->ErrorInfo;
return false;
} else {
$this->error = "Message sent!";
return true;
}
```

Hidden above in the mesh of code is:

```php
$mail->ContentType = 'text/calendar';
```

By far the most important line to get PHPMailer sending an acceptable event to outlook calendar. It holds the key to unlocking all that code.
