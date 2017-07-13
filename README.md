![Zenvia Logo](https://login.zenvia.com/Login_files/logo.png)

# Zenvia SMS Core for NodeJS

Under construction!

Full and official implementation of Zenvia SMS API, send, monitor status and receive SMS from clients with this module.

##### Full documentation about Zenvia API on http://docs.zenviasms.apiary.io

### Install
`npm install zenvia-sms-core` not available!

### How to create Zenvia SMS Callbacks Server

```javascript
let zenvia_cs = require('zenvia-sms-core').callbacksServer;

zenvia_cs.startServer(81);

zenvia_cs.events.on('event', (data)=>{
    console.log(data);
});
```

### How to use Zenvia SMS API

```javascript
/**
 * Zenvia SMS API - Usage Examples
 *
 * Functions:
 *      setCredentials(account, token) - Set API Credentials
 *      sendSMS(payload) - Send unique and multiple SMS
 *      getSMSStatus(sms_id) - Get SMS status by ID
 *      getSMSReceivedList() - Get received SMS list
 *      getSMSReceivedListSearch(start_date, end_date) - Get received SMS list filtered by start and end date
 *      cancelScheduledSMS(sms_id) - Cancel scheduled SMS by id
 *
 */

const zapi = require('zenvia-sms-core').api;

zapi.setCredentials('account', 'token');

/* Send unique short and long SMS example
 */
let send_sms_payload = {
    sendSmsRequest: {
        from: "Zenvia",
        to: "5551999999999",
        schedule: null,
        msg: "Hello Zenvia from NodeJS!!!",
        callbackOption: "ALL",
        id: '001',
        aggregateId: "002"
    }
};

zapi
    .sendSMS(send_sms_payload)
    .then((res)=> {
        console.log(res);
    })
    .catch((err)=> {
        console.error(err);
    });

/*
 Send multiple SMS example
 */
let send_multi_sms_payload = {
    sendSmsMultiRequest: {
        aggregateId: 1750,
        sendSmsRequestList: [
            {
                from: "Zenvia",
                to: "5551999999999",
                schedule: null,
                msg: "Hello Zenvia from NodeJS!!! 2",
                callbackOption: "ALL",
                id: '001'
            },
            {
                from: "Zenvia",
                to: "5551982193388",
                schedule: null,
                msg: "Hello Zenvia from NodeJS!!! 2",
                callbackOption: "ALL",
                id: '001'
            }
        ]
    }
};

zapi
    .sendSMS(send_multi_sms_payload)
    .then((res)=> {
        console.log(JSON.stringify(res));
    })
    .catch((err)=> {
        console.error(err);
    });
```

### For full examples see on `code_examples/` in this project.

# Development

### Make tests
for success send SMS tests case in api, fill `phone_number`, `zenvia_account`, `zenvia_token` on `test/api.test.js`.

run `npm test`.

### To Do
- create full examples to getSMSStatus, getSMSReceivedList, getSMSReceivedListSearch, cancelScheduledSMS
- getSMSStatus not working, possible Zenvia API bug
- getSMSReceivedList not working, possible Zenvia API bug
- getSMSReceivedListSearch not working, possible Zenvia API bug
- make callbacksServer unit tests
- Review license
- Review english

#### Under MIT License