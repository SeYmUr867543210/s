<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    
    <div class="canvas">
        <svg width="1000"height="1000">
            <rect></rect>
        </svg>
    </div>
    <script>
        firebase.initializeApp(config);
        const db = firebase.firestore();
    </script>
    
    <script src="https://d3js.org/d3.v5.js"></script>
    <script src="index.js"></script>
</body>
</html>



//priglasil svg
const svg = d3.select("svg");

//vzyat data s json
d3.json("menu.json").then(data=>{
    //nahodit min max iz json fiyla
    let min = d3.min(data ,d=> d.orders);
    let max = d3.max(data ,d=> d.orders);
//ogranichit po vysote /2  odinakogo vse bary
let y = d3.scaleLinear()
            .domain([0,d3.max(data ,d=> d.orders)])
            .range([0,500])
//ogranichivat po shyrine /2 odinakogo vse bary            
let x = d3.scaleBand()
            .domain(data.map(item=>item.name)) //vzyat koordinaty kazhdogo bara(s kotorogo nachinaetsya shirina)
            .range([0,100])                    //delit na 2 odinakogo vse bary mezhdu soboy
            .paddingInner(0.02)                //paddingInner - otstut vnutrenniy,paddingOuter - vneshniy otstup
            console.log(x("veg pasta"))
//vybiraem vse tagi rect           
const rects = svg.selectAll("rect")
            .data(data)
      //attributy dlya tagov rect kotoryye vnutri html
      rects.attr("height",d=>y(d.orders))
        .attr("width",x.bandwidth)      //shirina razdelennaya porovnu mezhdu vsemi barami
        .attr("fill","orange")
        .attr("x",d=> x(d.name))        //nachalo koordinat bara(shirina)
      //attributy dlya virtualnyh tagov rect kotoryyh eshe net html,no est data dlya nih v fayle json
      rects.enter()
        .append("rect")
        .attr("height",d=>y(d.orders))
        .attr("width",x.bandwidth)      
        .attr("fill","orange")
        .attr("x",d=> x(d.name))

 

})




[
    {
        "name": "veg soup",
        "orders": 200
    },
    {
        "name": "veg curry",
        "orders": 600
    },
    {
        "name": "veg pasta",
        "orders": 300
    },
    {
        "name": "veg surprise",
        "orders": 100
    },
    {
        "name": "veg sdf",
        "orders": 800
    },
    {
        "name": "veg fdfd",
        "orders": 850
    },
    {
        "name": "veg surwefwprise",
        "orders": 900
    }
]
