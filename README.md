# Crea el servicio

ng g service services/task
ng g interface interfaces/task 

# Tipar datos, atributos de una tarea (buena practica)
export interface Task {
    userId: string;
    id: string;
    tittle: string;
    completed: boolean
}

# Importo el modulo en aap.modules.ts
import { HttpClientModule } from '@angular/common/http';

# Importo dependencia HttpClient en task.services
import {HttpClient } from '@angular/common/http';

import { Task } from './../interfaces/task.model';

# Inyecto la clase contructor
constructor(private http: HttpClient) { }

# Importos nuestro servicio creado app.component.ts
import { TaskService } from './services/task.service';
constructor(private taskService: TaskService){}

# Solictud metodo Get y devuelve array de objetos Task, en un tipado, task.service.ts
getAllTasks(){
    const path = 'https://jsonplaceholder.typicode.com/todos';
    return this.http.get<Task[]>(path); 
}

# Lo mandamos a llamar en app.component.ts
getAllTasks(){
    this.taskService.getAllTasks()
    .subscribe(todos => {
        console.log(todos);
    })
}

# getAllTasks lo ejecuto con un btn en la plantilla HTML
<button (click)="getAllTasks()">getAllTasks()</button>

# getTask obtengo solo una tarea
getTask(id: string){
    const path = `https://jsonplaceholder.typicode.com/todos/${id}`
    return this.http.get<Task>(path);
}

# Conecto a mi componente
getTask(){
    this.taskService.getTask('1')
    .subscribe(todo => {
        console.log(todo);
    })
}

# btn para mi tarea
<button (click)="getTask()">getTask()</button>

# Creo variable privada
private api = 'https://jsonplaceholder.typicode.com'

# Metodo para crear tarea
createTask(task: Task){
    const path = `${this.api}/todos/`;
    return this.http.post(path,task);
}

# Crear Tarea
createTask(){
    const task = {
        id: '12',
        userId: '1',
        title: 'change title',
        completed: true
    };
    this.taskService.createTask(task)
    .subscribe((newTask) => {
        console.log(newTask);
    });
}

# btn para crear tarea
<button (click)="createTask()">createTask()</button>

# Metod update a la tarea
updateTask(task: Task){
    const path = `${this.api}/todos/${task.id}`;
    return this.http.put<Task>(path, task);
}

# Actualizar tarea
updateTask(){
    const task = {
        id: '201',
        userId: '1',
        title: 'change title',
        completed: true
    };
    this.taskService.updateTask(task)
    .subscribe(todo => {
        console.log(todo);
    })
}

# btn actualizar
<button (click)="updateTask()">updateTask()</button>

# Metodo borrar
deleteTask(id: string){
    const path = `${this.api}/todos/${task.id}`;
    return this.http.delete(path);
}

# Borrar tarea
deleteTask(){
    this.taskService.deleteTask('2')
    .subscribe(data => {
        console.log(data);
    });
  }
















# angular-http-client

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 9.1.8.

## Development server

Run `ng serve` for a dev server. Navigate to `http://localhost:4200/`. The app will automatically reload if you change any of the source files.

## Code scaffolding

Run `ng generate component component-name` to generate a new component. You can also use `ng generate directive|pipe|service|class|guard|interface|enum|module`.

## Build

Run `ng build` to build the project. The build artifacts will be stored in the `dist/` directory. Use the `--prod` flag for a production build.

## Running unit tests

Run `ng test` to execute the unit tests via [Karma](https://karma-runner.github.io).

## Running end-to-end tests

Run `ng e2e` to execute the end-to-end tests via [Protractor](http://www.protractortest.org/).

## Further help

To get more help on the Angular CLI use `ng help` or go check out the [Angular CLI README](https://github.com/angular/angular-cli/blob/master/README.md).
