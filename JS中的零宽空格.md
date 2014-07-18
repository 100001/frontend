
    var a = '\uFEFF';
    var b = 'b';
    var c = 'c';
    var d = (b+a+c);
    console.log(d);//bc
    console.log(d.length);//3
    var e = d.indexOf(a);
    console.log(e);//1