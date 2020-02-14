const cardsApp = {};

cardsApp.init = function(){
    cardsApp.flip();
    cardsApp.randomWord();
    cardsApp.newWordButton();
    cardsApp.cardCounterCalculater();
};

let cardCounter = 1;

let wordList = [
    {gaidhlig: 'Shin sibh!',
    gaidhligSentence: '"Shin sibh Siùsaidh!"',
    english: 'Hello there!',
    englishSentence: '"Hello there Susan!"'},
    {gaidhlig: 'Mar sin leat!',
    gaidhligSentence: '"Mar sin leat Daibhidh!"',
    english: 'Goodbye for now!',
    englishSentence: '"Goodbye for now David!"'},
    {gaidhlig: 'athair',
    gaidhligSentence: '"Tha athair cadalach."',
    english: 'father',
    englishSentence: '"Father is sleepy."'},
    {gaidhlig: 'màthair',
    gaidhligSentence: '"Tha màthair cadalach."',
    english: 'mother',
    englishSentence: '"Mother is sleepy."'},
    {gaidhlig: 'piuthar',
    gaidhligSentence: '"Tha piuthar agam."',
    english: 'sister',
    englishSentence: '"I have a sister."'},
    {gaidhlig: 'bràthair',
    gaidhligSentence: '"Tha bràthair agam."',
    english: 'brother',
    englishSentence: '"I have a brother."'},
    {gaidhlig: 'latha',
    gaidhligSentence: '"Tha latha 24 uair."',
    english: 'day',
    englishSentence: '"A day has 24 hours."'},
    {gaidhlig: 'seachdain',
    gaidhligSentence: '"Tha seachdain 7 latha."',
    english: 'week',
    englishSentence: '"A week has 7 days."'},
    {gaidhlig: 'mìos',
    gaidhligSentence: '"Is e mìos fuar a tha seo."',
    english: 'month',
    englishSentence: '"This is a cold month."'},
    {gaidhlig: 'bliadhna',
    gaidhligSentence: '"Am-bliadhna tha 2020."',
    english: 'year',
    englishSentence: '"This year is 2020."'},
    {gaidhlig: 'madainn',
    gaidhligSentence: '"Tha e madainn."',
    english: 'morning',
    englishSentence: '"It is morning."'},
    {gaidhlig: 'feasgar',
    gaidhligSentence: '"Tha e feasgar."',
    english: 'afternoon',
    englishSentence: '"It is afternoon."'},
    {gaidhlig: 'oidhche',
    gaidhligSentence: '"Tha an oidhche ann."',
    english: 'night',
    englishSentence: '"It is night."'},
    {gaidhlig: 'an-diugh',
    gaidhligSentence: '"Tha an latha an-diugh blàth."',
    english: 'today',
    englishSentence: '"Today is warm."'},
    {gaidhlig: 'an-dè',
    gaidhligSentence: '"Bha an-dè fuar."',
    english: 'yesterday',
    englishSentence: '"Yesterday was cold."'},
    {gaidhlig: 'a-màireach',
    gaidhligSentence: '"Bidh a-màireach teth."',
    english: 'tomorrow',
    englishSentence: '"Tomorrow will be hot."'},
    {gaidhlig: 'an t-uisge',
    gaidhligSentence: '"Tha an t-uisge ann."',
    english: 'rain',
    englishSentence: '"It is raining."'},
    {gaidhlig: 'gaothach',
    gaidhligSentence: '"Tha e gaothach."',
    english: 'windy',
    englishSentence: '"It is windy."'},
    {gaidhlig: 'ciùin',
    gaidhligSentence: '"Tha an latha ciùin."',
    english: 'calm',
    englishSentence: '"The day is calm."'},
    {gaidhlig: 'grianach',
    gaidhligSentence: '"Tha an latha an-diugh grianach."',
    english: 'sunny',
    englishSentence: '"Today is sunny."'},
    {gaidhlig: 'blàth',
    gaidhligSentence: '"Tha an latha an-diugh blàth."',
    english: 'warm',
    englishSentence: '"Today is warm."'},
    {gaidhlig: 'teth',
    gaidhligSentence: '"Tha an latha an-diugh teth."',
    english: 'hot',
    englishSentence: '"Today is hot."'},
    {gaidhlig: 'fuar',
    gaidhligSentence: '"Tha an latha an-diugh fuar."',
    english: 'cold',
    englishSentence: '"Today is cold."'},
];

const name = prompt(`Dè an t-ainm a th'ort? What is your name?`);

cardsApp.randomWord= function() {
    let word= wordList[Math.floor(Math.random()*wordList.length)];
    const gaidhligWord = word.gaidhlig;
    const gaidhligSentence = word.gaidhligSentence;
    $('.front').append(`<p class='displayGaidhlig'>${gaidhligWord} <br> <br>${gaidhligSentence}</p>`);
    const englishWord = word.english;
    const englishSentence = word.englishSentence;
    $('.back').append(`<p class='displayEnglish'>${englishWord} <br> <br>${englishSentence}</p>`);
    if (wordList.length > 1) {
        wordList = (wordList.filter(item => item !== word));
    } else {
        $('.newWord').attr('disabled', 'disabled');
        alert(`That's all for now!`);
    }  
};

cardsApp.newWordButton = function() {
    $('.newWord').on('click', function(){
        $('.displayGaidhlig').remove();
        $('.displayEnglish').remove();
        $('.card .back').addClass('hidden');
        cardsApp.randomWord();
        cardsApp.updateCardCounter();
    });
};


cardsApp.flip = function() {
    const front = function () {
        $('.card .front').on('click', function() {
            $(this).next().toggleClass('hidden');
        });
    };
    const back = function() {
        $('.card .back').on('click', function() {
            $(this).toggleClass('hidden');
        });
    };
    
    front();
    back();
}

cardsApp.cardCounterCalculater = function (){
    $('.cardCount p').text(`Shin sibh ${name}, you have learned ${cardCounter} word!`);
}

cardsApp.updateCardCounter = function() {
    cardCounter = cardCounter + 1;
    $('.cardCount p').text(`Shin sibh ${name}, you have learned ${cardCounter} words!`);
}


$(function(){
    cardsApp.init();
})