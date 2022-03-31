# flutter_midle_tabbar
flutter 中间弹出tabbar


///使用flutter实现底部中间按钮突出显示
import 'package:flutter/material.dart';


void main() => runApp(MyApp());

class MyApp extends StatelessWidget {
  const MyApp({Key? key}) : super(key: key);

  // This widget is the root of your application.
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: const TabNavigator(),
    );
  }
}

class HomePage extends StatefulWidget {
  @override
  State<StatefulWidget> createState() => _HomePageState();
}

class _HomePageState extends State<HomePage> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      // backgroundColor: Colors.red,
      appBar: AppBar(
        backgroundColor: const Color.fromRGBO(220, 220, 220, 1.0),
        title: const Text('hello'),
        centerTitle: true,
        elevation: 0.0,
      ),
    );
  }
}

class TabNavigator extends StatefulWidget {
  const TabNavigator({Key? key}) : super(key: key);

  @override
  State<StatefulWidget> createState() => _TabNavigatorState();
}

class _TabNavigatorState extends State<TabNavigator> {
  final _defaultColor = Colors.grey;
  final _activeColor = Colors.green[500];
  final int _currentIndex = 0;
  final PageController _controller = PageController(
    initialPage: 0,
  );

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      // appBar: AppBar(title: Text('123'),),
      body: PageView(
        controller: _controller,
        children: <Widget>[
          HomePage(),
        ],
        physics: const NeverScrollableScrollPhysics(),
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: (){},
        tooltip: 'Increment',
        child: const Icon(Icons.add),
        elevation: 4.0,
      ),
      bottomNavigationBar: BottomAppBar(
        child: Row(
          mainAxisAlignment: MainAxisAlignment.center,
          children: <Widget>[
            Expanded(child:  IconButton(icon: const Icon(Icons.home), onPressed: (){  },),),
             Expanded(child: IconButton(icon: Icon(Icons.show_chart), onPressed: (){  },),),
            const Expanded(child: Text('')),
            Expanded(child: IconButton(icon:  Icon(Icons.tab), onPressed: () {  },),),
             Expanded(child: IconButton(icon: const Icon(Icons.settings), onPressed: (){  },),),
          ],
        ),
      ),
      floatingActionButtonLocation: FloatingActionButtonLocation.centerDocked,
    );
  }

  _bottomItem(String title, IconData icon, int index) {
    return BottomNavigationBarItem(
      icon: Icon(
        icon,
        color: _defaultColor,
      ),
      activeIcon: Icon(
        icon,
        color: _activeColor,
      ),
      title: Text(
        title,
        style: TextStyle(
            color: _currentIndex != index ? _defaultColor : _activeColor),
      ),
    );
  }
}


