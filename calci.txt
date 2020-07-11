import 'package:flutter/cupertino.dart';
import 'package:flutter/material.dart';

void main() {
  runApp(myapp());
}

class myapp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: "Calculator",
      theme: ThemeData(primarySwatch: Colors.red),
      home: HomePage(),
    );
  }
}

class HomePage extends StatefulWidget {
  @override
  _HomePageState createState() => _HomePageState();
}

class _HomePageState extends State<HomePage> {
  int firstnum;
  int secondnum;
  String texttodisplay = "";
  String res;
  String operatortoperform;
  void btnclicked(String btnval) {
    if (btnval == "C") {
      texttodisplay = "";
      firstnum = 0;

      secondnum = 0;
      res = "";
    } else if (btnval == "+" ||
        btnval == "-" ||
        btnval == "x" ||
        btnval == "/") {
      firstnum = int.parse(texttodisplay);
      res = "";
      operatortoperform = btnval;
    } else if (btnval == "=") {
      secondnum = int.parse(texttodisplay);
      if (operatortoperform == "+") {
        res = (firstnum + secondnum).toString();
      }
      if (operatortoperform == "-") {
        res = (firstnum - secondnum).toString();
      }
      if (operatortoperform == "x") {
        res = (firstnum * secondnum).toString();
      }
      if (operatortoperform == "/") {
        res = (firstnum ~/ secondnum).toString();
      }
    } else {
      res = int.parse(texttodisplay + btnval).toString();
    }
    setState(() {
      texttodisplay = res;
    });
  }

  Widget custombutton(String btnval) {
    return Expanded(
      child: OutlineButton(
        borderSide: BorderSide(
          color: Colors.black,
          width: 1,
        ),
        splashColor: Colors.lightBlueAccent,
        highlightElevation: 20,
        padding: EdgeInsets.all(20),
        onPressed: () => btnclicked(btnval),
        child: Text(
          "$btnval",
          style: TextStyle(fontSize: 25.0),
        ),
      ),
    );
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        centerTitle: true,
        title: Text(
          "MY CALCULATOR",
        ),
      ),
      body: Container(
        child: Column(
          mainAxisAlignment: MainAxisAlignment.end,
          children: <Widget>[
            Expanded(
              child: Container(
                  padding: EdgeInsets.all(6),
                  alignment: Alignment.bottomRight,
                  child: Text(
                    "$texttodisplay",
                    style: TextStyle(fontSize: 35, fontWeight: FontWeight.w600),
                  )),
            ),
            Row(
              children: <Widget>[
                custombutton("9"),
                custombutton("8"),
                custombutton("7"),
                custombutton("+")
              ],
            ),
            Row(
              children: <Widget>[
                custombutton("6"),
                custombutton("5"),
                custombutton("4"),
                custombutton("-")
              ],
            ),
            Row(
              children: <Widget>[
                custombutton("3"),
                custombutton("2"),
                custombutton("1"),
                custombutton("x")
              ],
            ),
            Row(
              children: <Widget>[
                custombutton("0"),
                custombutton("C"),
                custombutton("="),
                custombutton("/")
              ],
            ),
          ],
        ),
      ),
    );
  }
}
