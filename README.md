# Qoutex-vip-bot
Official bot
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width,initial-scale=1.0">
<title>Cortex DP Bot</title>

<style>
*{box-sizing:border-box}

body{
    margin:0;
    min-height:100vh;
    background:
      radial-gradient(circle at 50% 0%,#242424 0%,#080808 42%,#000 100%);
    color:#fff;
    font-family:Arial,Helvetica,sans-serif;
    overflow-x:hidden;
}

.snow{
    position:fixed;
    inset:0;
    pointer-events:none;
    opacity:.28;
    background-image:
      radial-gradient(2px 2px,#fff,transparent),
      radial-gradient(1px 1px,#fff,transparent),
      radial-gradient(1.5px 1.5px,#fff,transparent);
    background-size:80px 80px,45px 45px,110px 110px;
    animation:snowfall 12s linear infinite;
    z-index:0;
}

@keyframes snowfall{
    from{
        background-position:0 0,20px 20px,60px 10px;
    }
    to{
        background-position:0 240px,80px 300px,120px 250px;
    }
}

.app{
    position:relative;
    z-index:2;
    width:min(560px,94%);
    margin:auto;
    padding:22px 0 45px;
}

.header{
    text-align:center;
    padding:28px 15px;
    border-radius:28px;
    border:1px solid #303030;
    background:linear-gradient(145deg,#171717,#050505);
    box-shadow:0 0 45px rgba(225,181,64,.12);
}

.logo{
    font-size:76px;
    line-height:1;
    animation:lionPulse 2s infinite;
    filter:drop-shadow(0 0 18px rgba(255,200,50,.3));
}

@keyframes lionPulse{
    0%,100%{transform:scale(1)}
    50%{transform:scale(1.08)}
}

.title{
    margin-top:13px;
    font-size:31px;
    font-weight:1000;
    letter-spacing:2px;
}

.gold{color:#e6bd54}

.status{
    margin-top:12px;
    color:#00ff9d;
    font-size:13px;
    font-weight:bold;
}

.panel{
    margin-top:16px;
    padding:18px;
    border-radius:22px;
    border:1px solid #292929;
    background:#0d0d0d;
}

label{
    display:block;
    color:#999;
    font-size:12px;
    margin:0 0 7px;
}

input,select{
    width:100%;
    padding:14px;
    border-radius:13px;
    border:1px solid #333;
    outline:none;
    background:#050505;
    color:#fff;
    font-size:15px;
}

.row{
    display:grid;
    grid-template-columns:1fr 1fr;
    gap:10px;
    margin-top:12px;
}

button{
    width:100%;
    padding:15px;
    margin-top:12px;
    border:0;
    border-radius:14px;
    cursor:pointer;
    font-size:15px;
    font-weight:900;
    background:linear-gradient(135deg,#a77b28,#edcc6c);
    color:#090909;
}

button.secondary{
    background:#202020;
    color:#fff;
    border:1px solid #333;
}

button.ai{
    font-size:17px;
    margin-top:14px;
}

.signal{
    margin-top:17px;
    padding:28px 15px;
    text-align:center;
    border-radius:24px;
    border:1px solid #303030;
    background:#050505;
}

.signalText{
    font-size:58px;
    line-height:1;
    font-weight:1000;
    letter-spacing:3px;
}

.up{color:#00ff9d}
.down{color:#ff4545}
.wait{color:#e6bd54}

.confidence{
    margin-top:12px;
    font-size:19px;
}

.countdown{
    margin-top:14px;
    color:#e6bd54;
    font-size:28px;
    font-weight:900;
}

.reason{
    margin-top:13px;
    color:#999;
    font-size:13px;
    line-height:1.5;
}

.grid{
    display:grid;
    grid-template-columns:1fr 1fr;
    gap:10px;
    margin-top:17px;
}

.box{
    padding:14px;
    border-radius:15px;
    border:1px solid #282828;
    background:#0c0c0c;
}

.box small{
    color:#777;
    font-size:10px;
}

.box strong{
    display:block;
    margin-top:7px;
    font-size:14px;
}

.log{
    margin-top:15px;
    max-height:150px;
    overflow:auto;
    color:#888;
    font-size:11px;
    line-height:1.7;
}

.footer{
    text-align:center;
    color:#555;
    font-size:10px;
    margin-top:20px;
}

.otcNote{
    color:#ffcc66;
    font-size:11px;
    line-height:1.5;
    margin-top:10px;
}

@media(max-width:430px){
    .row{grid-template-columns:1fr}
    .signalText{font-size:50px}
}
</style>
</head>

<body>

<div class="snow"></div>

<div class="app">

<!-- HEADER -->

<div class="header">

    <div class="logo">🦁</div>

    <div class="title">
        CORTEX <span class="gold">DP BOT</span>
    </div>

    <div id="status" class="status">
        ● DISCONNECTED
    </div>

</div>


<!-- CONNECTION PANEL -->

<div class="panel">

    <label>TWELVE DATA API KEY</label>

    <input
        id="apiKey"
        type="password"
        placeholder="Paste API key"
    >

    <div class="row">

        <div>
            <label>MARKET TYPE</label>

            <select id="marketType"
                    onchange="marketChanged()">

                <option value="LIVE">
                    LIVE FOREX
                </option>

                <option value="OTC">
                    OTC FEED
                </option>

            </select>
        </div>

        <div>
            <label>PAIR</label>

            <select id="symbol">

                <option>EUR/USD</option>
                <option>GBP/USD</option>
                <option>USD/JPY</option>
                <option>USD/CHF</option>
                <option>AUD/USD</option>
                <option>USD/CAD</option>
                <option>NZD/USD</option>
                <option>EUR/JPY</option>
                <option>GBP/JPY</option>

            </select>
        </div>

    </div>


    <div id="otcBox" style="display:none;margin-top:12px">

        <label>
            AUTHORIZED OTC WEBSOCKET URL
        </label>

        <input
            id="otcUrl"
            type="text"
            placeholder="wss://your-authorized-otc-feed"
        >

        <div class="otcNote">
            OTC mode requires a legitimate/authorized
            OTC data feed. This bot does not generate
            fake OTC prices.
        </div>

    </div>


    <div class="row">

        <div>
            <label>TIMEFRAME</label>

            <select id="timeframe">

                <option value="60">
                    1 MINUTE
                </option>

            </select>
        </div>

        <div>
            <label>SIGNAL LOCK</label>

            <select disabled>

                <option>
                    60 SECONDS
                </option>

            </select>
        </div>

    </div>


    <button onclick="connectBot()">
        ⚡ CONNECT MARKET
    </button>

    <button
        class="secondary"
        onclick="disconnectBot()"
    >
        ■ STOP BOT
    </button>

    <button
        class="ai"
        onclick="aiAnalysis()"
    >
        🤖 AI ANALYSIS
    </button>

</div>


<!-- SIGNAL -->

<div class="signal">

    <div
        id="signal"
        class="signalText wait"
    >
        WAIT
    </div>

    <div class="confidence">
        Confidence:
        <strong id="confidence">0%</strong>
    </div>

    <div
        id="countdown"
        class="countdown"
    >
        READY
    </div>

    <div
        id="reason"
        class="reason"
    >
        Connect market data. The bot scans
        completed 1-minute candles.
    </div>

</div>


<!-- INDICATORS -->

<div class="grid">

    <div class="box">
        <small>PRICE</small>
        <strong id="price">--</strong>
    </div>

    <div class="box">
        <small>EMA 9</small>
        <strong id="ema9">--</strong>
    </div>

    <div class="box">
        <small>EMA 21</small>
        <strong id="ema21">--</strong>
    </div>

    <div class="box">
        <small>RSI 14</small>
        <strong id="rsi">--</strong>
    </div>

    <div class="box">
        <small>MARKET STRUCTURE</small>
        <strong id="structure">--</strong>
    </div>

    <div class="box">
        <small>FVG</small>
        <strong id="fvg">--</strong>
    </div>

    <div class="box">
        <small>ORDER BLOCK</small>
        <strong id="ob">--</strong>
    </div>

    <div class="box">
        <small>LIQUIDITY</small>
        <strong id="liquidity">--</strong>
    </div>

</div>


<!-- LOG -->

<div class="panel">

    <b>📊 CORTEX ANALYSIS LOG</b>

    <div
        id="log"
        class="log"
    ></div>

</div>


<div class="footer">
    CORTEX DP BOT • 1 MIN LIVE MARKET SCANNER
</div>

</div>


<script>

/* =====================================================
   GLOBAL VARIABLES
===================================================== */

let ws = null;

let running = false;

let candles = [];

let currentCandle = null;

let ticks = [];

let lastMinute = null;

let signalLocked = false;

let lockUntil = 0;

let activeSignal = null;


/* =====================================================
   AUDIO
===================================================== */

function speak(text){

    try{

        window.speechSynthesis.cancel();

        const voice =
            new SpeechSynthesisUtterance(text);

        voice.rate = .85;
        voice.pitch = .7;
        voice.volume = 1;

        window.speechSynthesis.speak(voice);

    }catch(e){}

}


function beep(){

    try{

        const ctx =
            new (window.AudioContext ||
                 window.webkitAudioContext)();

        const osc =
            ctx.createOscillator();

        const gain =
            ctx.createGain();

        osc.frequency.value = 650;

        gain.gain.value = .08;

        osc.connect(gain);

        gain.connect(ctx.destination);

        osc.start();

        osc.stop(
            ctx.currentTime + .25
        );

    }catch(e){}

}


/* =====================================================
   LOG
===================================================== */

function log(text){

    const box =
        document.getElementById("log");

    const time =
        new Date().toLocaleTimeString();

    box.innerHTML =
        `<div>[${time}] ${text}</div>` +
        box.innerHTML;
}


/* =====================================================
   MARKET TYPE
===================================================== */

function marketChanged(){

    const type =
        document.getElementById(
            "marketType"
        ).value;

    document.getElementById(
        "otcBox"
    ).style.display =
        type === "OTC"
        ? "block"
        : "none";

}


/* =====================================================
   CONNECT
===================================================== */

function connectBot(){

    disconnectBot();

    const type =
        document.getElementById(
            "marketType"
        ).value;

    if(type === "LIVE"){

        connectLive();

    }else{

        connectOTC();

    }

}


/* =====================================================
   LIVE TWELVE DATA
===================================================== */

function connectLive(){

    const key =
        document.getElementById(
            "apiKey"
        ).value.trim();

    const symbol =
        document.getElementById(
            "symbol"
        ).value;

    if(!key){

        alert(
            "Twelve Data API key enter karo."
        );

        return;
    }


    setStatus(
        "● CONNECTING LIVE MARKET"
    );


    const url =
        "wss://ws.twelvedata.com/v1/quotes/price" +
        "?apikey=" +
        encodeURIComponent(key);


    ws =
        new WebSocket(url);


    ws.onopen = function(){

        running = true;

        setStatus(
            "● LIVE MARKET CONNECTED"
        );

        ws.send(
            JSON.stringify({

                action:"subscribe",

                params:{
                    symbols:symbol
                }

            })
        );

        log(
            "LIVE CONNECTED: " + symbol
        );

        speak(
            "Cortex DP Bot live market connected"
        );

    };


    ws.onmessage = function(event){

        try{

            const data =
                JSON.parse(event.data);

            if(
                data.price !== undefined &&
                data.price !== null
            ){

                const price =
                    Number(data.price);

                const timestamp =
                    data.timestamp
                    ? Number(data.timestamp) * 1000
                    : Date.now();

                processTick(
                    price,
                    timestamp
                );

            }

        }catch(error){

            console.log(
                "Tick error",
                error
            );

        }

    };


    ws.onerror = function(){

        setStatus(
            "● CONNECTION ERROR"
        );

        log(
            "Live market connection error"
        );

    };


    ws.onclose = function(){

        if(running){

            setStatus(
                "● LIVE DISCONNECTED"
            );

        }

    };

}


/* =====================================================
   OTC CONNECTOR
===================================================== */

function connectOTC(){

    const otcUrl =
        document.getElementById(
            "otcUrl"
        ).value.trim();


    if(!otcUrl){

        alert(
            "Authorized OTC WebSocket URL enter karo."
        );

        return;
    }


    if(
        !otcUrl.startsWith("wss://") &&
        !otcUrl.startsWith("ws://")
    ){

        alert(
            "Valid WebSocket URL enter karo."
        );

        return;
    }


    setStatus(
        "● CONNECTING OTC"
    );


    ws =
        new WebSocket(otcUrl);


    ws.onopen = function(){

        running = true;

        setStatus(
            "● OTC FEED CONNECTED"
        );

        log(
            "Authorized OTC feed connected"
        );

    };


    /*
       Different OTC providers send
       different JSON formats.

       Supported examples:

       {"price":1.12345}

       {"price":1.12345,"timestamp":123456789}

       {"data":{"price":1.12345}}
    */

    ws.onmessage = function(event){

        try{

            let data =
                JSON.parse(event.data);


            let price = null;

            let timestamp =
                Date.now();


            if(
                typeof data.price === "number"
            ){

                price = data.price;

            }


            if(
                data.data &&
                typeof data.data.price === "number"
            ){

                price =
                    data.data.price;

            }


            if(
                data.timestamp
            ){

                timestamp =
                    Number(data.timestamp);

                if(timestamp < 10000000000){

                    timestamp *= 1000;

                }

            }


            if(price !== null){

                processTick(
                    Number(price),
                    timestamp
                );

            }

        }catch(e){

            console.log(
                "OTC message:",
                event.data
            );

        }

    };


    ws.onerror = function(){

        setStatus(
            "● OTC CONNECTION ERROR"
        );

        log(
            "OTC feed connection error"
        );

    };


    ws.onclose = function(){

        if(running){

            setStatus(
                "● OTC DISCONNECTED"
            );

        }

    };

}


/* =====================================================
   TICK → ONE MINUTE CANDLE
===================================================== */

function processTick(
    price,
    timestamp
){

    document.getElementById(
        "price"
    ).innerText =
        Number(price).toFixed(5);


    const minute =
        Math.floor(
            timestamp / 60000
        ) * 60000;


    if(
        currentCandle === null
    ){

        currentCandle = {

            time:minute,

            open:price,

            high:price,

            low:price,

            close:price

        };

        lastMinute = minute;

        return;

    }


    /*
       NEW MINUTE STARTED

       Previous candle is now complete.
    */

    if(
        minute !==
        currentCandle.time
    ){

        closeCandle();


        currentCandle = {

            time:minute,

            open:price,

            high:price,

            low:price,

            close:price

        };

        lastMinute = minute;

        return;

    }


    currentCandle.high =
        Math.max(
            currentCandle.high,
            price
        );

    currentCandle.low =
        Math.min(
            currentCandle.low,
            price
        );

    currentCandle.close =
        price;

}


/* =====================================================
   CLOSE CANDLE
===================================================== */

function closeCandle(){

    if(!currentCandle)
        return;


    candles.push(
        currentCandle
    );


    if(candles.length > 150){

        candles.shift();

    }


    log(
        "1-minute candle completed"
    );


    /*
       MOST IMPORTANT RULE:

       If previous signal is locked,
       DO NOT create another signal.
    */

    if(signalLocked){

        log(
            "Signal locked — no new signal"
        );

        currentCandle = null;

        return;

    }


    const result =
        analyseMarket(
            candles
        );


    if(
        result.signal !== "WAIT"
    ){

        createSignal(
            result
        );

    }else{

        showWait(
            result.reason
        );

    }


    currentCandle = null;

}


/* =====================================================
   EMA
===================================================== */

function EMA(
    values,
    period
){

    if(
        values.length < period
    ){

        return null;

    }


    const multiplier =
        2 / (period + 1);


    let result =
        values
        .slice(0,period)
        .reduce(
            (a,b)=>a+b,
            0
        ) / period;


    for(
        let i=period;
        i<values.length;
        i++
    ){

        result =
            (
                values[i] -
                result
            ) *
            multiplier +
            result;

    }


    return result;

}


/* =====================================================
   RSI
===================================================== */

function RSI(
    values,
    period=14
){

    if(
        values.length <
        period + 1
    ){

        return null;

    }


    let gain = 0;

    let loss = 0;


    for(
        let i =
            values.length - period;
        i < values.length;
        i++
    ){

        const difference =
            values[i] -
            values[i-1];


        if(
            difference >= 0
        ){

            gain += difference;

        }else{

            loss +=
                Math.abs(
                    difference
                );

        }

    }


    if(loss === 0)
        return 100;


    const rs =
        (gain / period) /
        (loss / period);


    return (
        100 -
        100 / (1 + rs)
    );

}


/* =====================================================
   FVG
===================================================== */

function FVG(data){

    if(
        data.length < 3
    ){

        return "NONE";

    }


    const a =
        data[data.length-3];

    const c =
        data[data.length-1];


    if(
        c.low > a.high
    ){

        return "BULLISH";

    }


    if(
        c.high < a.low
    ){

        return "BEARISH";

    }


    return "NONE";

}


/* =====================================================
   ORDER BLOCK
===================================================== */

function ORDER_BLOCK(data){

    if(
        data.length < 4
    ){

        return "NONE";

    }


    const previous =
        data[data.length-2];

    const last =
        data[data.length-1];


    if(
        previous.close <
        previous.open &&
        last.close >
        last.open &&
        last.close >
        previous.high
    ){

        return "BULLISH";

    }


    if(
        previous.close >
        previous.open &&
        last.close <
        last.open &&
        last.close <
        previous.low
    ){

        return "BEARISH";

    }


    return "NONE";

}


/* =====================================================
   MARKET STRUCTURE
===================================================== */

function STRUCTURE(data){

    if(
        data.length < 8
    ){

        return "RANGE";

    }


    const recent =
        data.slice(-4);

    const old =
        data.slice(-8,-4);


    const recentHigh =
        Math.max(
            ...recent.map(
                c=>c.high
            )
        );

    const oldHigh =
        Math.max(
            ...old.map(
                c=>c.high
            )
        );


    const recentLow =
        Math.min(
            ...recent.map(
                c=>c.low
            )
        );

    const oldLow =
        Math.min(
            ...old.map(
                c=>c.low
            )
        );


    if(
        recentHigh > oldHigh &&
        recentLow > oldLow
    ){

        return "BULLISH";

    }


    if(
        recentHigh < oldHigh &&
        recentLow < oldLow
    ){

        return "BEARISH";

    }


    return "RANGE";

}


/* =====================================================
   LIQUIDITY
===================================================== */

function LIQUIDITY(data){

    if(
        data.length < 10
    ){

        return "NONE";

    }


    const recent =
        data.slice(-10);


    const highest =
        Math.max(
            ...recent.map(
                c=>c.high
            )
        );


    const lowest =
        Math.min(
            ...recent.map(
                c=>c.low
            )
        );


    const last =
        data[data.length-1];


    if(
        last.high >= highest
    ){

        return "BUY-SIDE";

    }


    if(
        last.low <= lowest
    ){

        return "SELL-SIDE";

    }


    return "NONE";

}


/* =====================================================
   ANALYSIS ENGINE
===================================================== */

function analyseMarket(data){

    if(
        data.length < 30
    ){

        return {

            signal:"WAIT",

            confidence:0,

            reason:
              "Collecting at least 30 candles"

        };

    }


    const closes =
        data.map(
            c=>c.close
        );


    const last =
        data[data.length-1];


    const ema9 =
        EMA(
            closes,
            9
        );


    const ema21 =
        EMA(
            closes,
            21
        );


    const rsi =
        RSI(
            closes,
            14
        );


    const structure =
        STRUCTURE(data);


    const fvg =
        FVG(data);


    const ob =
        ORDER_BLOCK(data);


    const liquidity =
        LIQUIDITY(data);


    let bullish = 0;

    let bearish = 0;


    /*
       EMA
    */

    if(
        last.close > ema9
    ){

        bullish += 1;

    }else{

        bearish += 1;

    }


    /*
       EMA TREND
    */

    if(
        ema9 > ema21
    ){

        bullish += 2;

    }else{

        bearish += 2;

    }


    /*
       RSI
    */

    if(
        rsi > 50 &&
        rsi < 70
    ){

        bullish += 1;

    }


    if(
        rsi < 50 &&
        rsi > 30
    ){

        bearish += 1;

    }


    /*
       MARKET STRUCTURE
    */

    if(
        structure === "BULLISH"
    ){

        bullish += 2;

    }


    if(
        structure === "BEARISH"
    ){

        bearish += 2;

    }


    /*
       FVG
    */

    if(
        fvg === "BULLISH"
    ){

        bullish += 2;

    }


    if(
        fvg === "BEARISH"
    ){

        bearish += 2;

    }


    /*
       ORDER BLOCK
    */

    if(
        ob === "BULLISH"
    ){

        bullish += 2;

    }


    if(
        ob === "BEARISH"
    ){

        bearish += 2;

    }


    /*
       LIQUIDITY
    */

    if(
        liquidity === "BUY-SIDE"
    ){

        bearish += 1;

    }


    if(
        liquidity === "SELL-SIDE"
    ){

        bullish += 1;

    }


    const total =
        bullish +
        bearish;


    if(!total){

        return {

            signal:"WAIT",

            confidence:0,

            reason:"No setup"

        };

    }


    let signal =
        "WAIT";


    if(
        bullish >
        bearish
    ){

        signal = "UP";

    }


    if(
        bearish >
        bullish
    ){

        signal = "DOWN";

    }


    /*
       Require a minimum difference.
       This prevents weak/random signals.
    */

    if(
        Math.abs(
            bullish - bearish
        ) < 2
    ){

        signal = "WAIT";

    }


    const confidence =
        Math.round(
            (
                Math.max(
                    bullish,
                    bearish
                ) /
                total
            ) * 100
        );


    return {

        signal,

        confidence:
            Math.min(
                confidence,
                95
            ),

        reason:
            `${structure} | FVG ${fvg} | OB ${ob} | Liquidity ${liquidity}`,

        indicators:{

            ema9:
                Number(
                    ema9.toFixed(5)
                ),

            ema21:
                Number(
                    ema21.toFixed(5)
                ),

            rsi:
                Number(
                    rsi.toFixed(2)
                ),

            structure,

            fvg,

            ob,

            liquidity

        }

    };

}


/* =====================================================
   CREATE SIGNAL
===================================================== */

function createSignal(result){

    /*
       HARD LOCK

       Only one signal can exist
       during the 60 second expiry.
    */

    if(signalLocked)
        return;


    signalLocked = true;

    activeSignal =
        result.signal;


    lockUntil =
        Date.now() +
        60000;


    showSignal(
        result
    );


    beep();


    speak(
        "Cortex DP Bot. " +
        result.signal +
        " signal. " +
        result.confidence +
        " percent confidence."
    );


    log(
        "NEW SIGNAL → " +
        result.signal +
        " | " +
        result.confidence +
        "%"
    );

}


/* =====================================================
   SIGNAL DISPLAY
===================================================== */

function showSignal(result){

    const el =
        document.getElementById(
            "signal"
        );


    el.innerText =
        result.signal;


    el.className =
        "signalText " +
        (
            result.signal === "UP"
            ? "up"
            : "down"
        );


    document.getElementById(
        "confidence"
    ).innerText =
        result.confidence +
        "%";


    document.getElementById(
        "reason"
    ).innerText =
        result.reason;


    if(
        result.indicators
    ){

        document.getElementById(
            "ema9"
        ).innerText =
            result.indicators.ema9;


        document.getElementById(
            "ema21"
        ).innerText =
            result.indicators.ema21;


        document.getElementById(
            "rsi"
        ).innerText =
            result.indicators.rsi;


        document.getElementById(
            "structure"
        ).innerText =
            result.indicators.structure;


        document.getElementById(
            "fvg"
        ).innerText =
            result.indicators.fvg;


        document.getElementById(
            "ob"
        ).innerText =
            result.indicators.ob;


        document.getElementById(
            "liquidity"
        ).innerText =
            result.indicators.liquidity;

    }

}


/* =====================================================
   WAIT
===================================================== */

function showWait(reason){

    const el =
        document.getElementById(
            "signal"
        );


    el.innerText =
        "WAIT";


    el.className =
        "signalText wait";


    document.getElementById(
        "confidence"
    ).innerText =
        "0%";


    document.getElementById(
        "reason"
    ).innerText =
        reason;

}


/* =====================================================
   COUNTDOWN
===================================================== */

setInterval(function(){

    if(!signalLocked){

        document.getElementById(
            "countdown"
        ).innerText =
            "SCANNING...";

        return;

    }


    const remaining =
        Math.max(
            0,
            Math.ceil(
                (
                    lockUntil -
                    Date.now()
                ) / 1000
            )
        );


    document.getElementById(
        "countdown"
    ).innerText =
        remaining > 0
        ? "SIGNAL ACTIVE • " +
          remaining +
          " SEC"
        : "SCANNING...";


    if(
        remaining <= 0
    ){

        signalLocked = false;

        activeSignal = null;

        lockUntil = 0;


        log(
            "Signal expired — scanner unlocked"
        );


        showWait(
            "Previous signal expired. Scanning next setup..."
        );

    }

},1000);


/* =====================================================
   AI ANALYSIS
===================================================== */

function aiAnalysis(){

    if(
        candles.length < 30
    ){

        speak(
            "AI analysis needs more market data."
        );

        log(
            "AI: Not enough candles."
        );

        return;

    }


    const result =
        analyseMarket(
            candles
        );


    if(
        result.signal === "WAIT"
    ){

        speak(
            "AI analysis complete. Wait."
        );

        log(
            "AI ANALYSIS → WAIT"
        );

        return;

    }


    speak(
        "AI analysis complete. " +
        result.signal +
        " signal."
    );


    log(
        "AI ANALYSIS → " +
        result.signal +
        " | " +
        result.confidence +
        "%"
    );

}


/* =====================================================
   STATUS
===================================================== */

function setStatus(text){

    document.getElementById(
        "status"
    ).innerText =
        text;

}


/* =====================================================
   DISCONNECT
===================================================== */

function disconnectBot(){

    running = false;


    if(ws){

        try{
            ws.close();
        }catch(e){}

        ws = null;

    }


    setStatus(
        "● DISCONNECTED"
    );


    log(
        "Bot stopped"
    );

}


/* =====================================================
   STARTUP
===================================================== */

window.addEventListener(
    "load",
    function(){

        log(
            "Cortex DP Bot ready"
        );

    }
);

</script>

</body>
</html>
