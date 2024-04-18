# trabalh
import 'package:flutter/material.dart';

void main() {
  runApp(MeuApp());
}

class MeuApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      title: 'Lista de Tarefas',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: TelaListaDeTarefas(),
      debugShowCheckedModeBanner: false, // Remover o banner de debug
    );
  }
}

class TelaListaDeTarefas extends StatefulWidget {
  @override
  _TelaListaDeTarefasState createState() => _TelaListaDeTarefasState();
}

class _TelaListaDeTarefasState extends State<TelaListaDeTarefas> {
  List<String> tarefas = [];

  void adicionarTarefa() {
    showDialog(
      context: context,
      builder: (BuildContext context) {
        String textoTarefa = '';
        return AlertDialog(
          title: Text('Adicionar Tarefa'),
          content: TextField(
            onChanged: (value) {
              textoTarefa = value;
            },
          ),
          actions: <Widget>[
            TextButton(
              child: Text('CANCELAR'),
              onPressed: () {
                Navigator.of(context).pop();
              },
            ),
            TextButton(
              child: Text('ADICIONAR'),
              onPressed: () {
                setState(() {
                  if (textoTarefa.isNotEmpty) {
                    tarefas.add(textoTarefa);
                  }
                });
                Navigator.of(context).pop();
              },
            ),
          ],
        );
      },
    );
  }

  void removerTarefa(int index) {
    setState(() {
      tarefas.removeAt(index);
    });
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Lista de Tarefas'),
      ),
      body: ListView.builder(
        itemCount: tarefas.length,
        itemBuilder: (context, index) {
          return Card(
            child: ListTile(
              title: Text(tarefas[index]),
              trailing: IconButton(
                icon: Icon(Icons.delete),
                onPressed: () {
                  removerTarefa(index);
                },
              ),
            ),
          );
        },
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: adicionarTarefa,
        child: Icon(Icons.add),
      ),
    );
  }
}
