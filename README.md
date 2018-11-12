# faster-api-deploy
wrapper over express

sample.

const RESTApi = require('faster-api-deploy');
const app = new RESTApi();

app.setErrorHandler((err, req, res, next) => {
    if (res.headerSent) {
        console.log('Response already sent hence sending error next');
        return next(err);
    }
    return res.status(500).json({
        msg: err.message ? err.message : err
    });
})

app.get("/hello", (req, res) => {
    res.status(200);

    return {
        message: "success"
    }
});

app.get("/he", async (req, res) => {
    await sleep(300);
    throw "ssssssssssssssssssssssss"
});

const sleep = (time) => {
    return new Promise((res, rej) => {
        setTimeout(res, time);
    });
};

// app.startListening(9000, "dev", "REST Api");

// it's picking info from .env file in root
app.startListening();


