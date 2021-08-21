# angular-custompipe

employee.ts

```js
export interface IEmployee {
  id: number;
  code: string;
  name: string;
  salary: number;
}
```

employee-component.component.ts

```js
import { Component, OnInit } from '@angular/core';
import { IEmployee } from './employee';

@Component({
  selector: 'app-employee-component',
  templateUrl: './employee-component.component.html',
  styleUrls: ['./employee-component.component.css']
})
export class EmployeeComponentComponent implements OnInit {
  constructor() {}

  ngOnInit() {}
  employees: IEmployee[] = [
    {
      id: 1,
      code: 'VOD-1410',
      name: 'Akshay Patel',
      salary: 3000
    },
    {
      id: 2,
      code: 'VOD-1710',
      name: 'Panth Patel',
      salary: 1500
    }
  ];
}
```

conver-to-spaces.pipe.ts

```js
import { Pipe, PipeTransform } from '@angular/core';

@Pipe({
  name: 'convertToSpaces'
})
export class ConvertToSpacesPipe implements PipeTransform {
  transform(value: string, charactor: string): string {
    return value.replace(charactor, ' ');
  }
}
```

employee-component.component.html

```html
<div *ngFor="let employee of employees">
  {{employee.id}} <br />
  {{employee.code | lowercase | convertToSpaces:'-'}} <br />
  {{employee.name | uppercase}} <br />
  {{employee.salary | currency:'USD':'symbol':'1.2-2' }}
  <hr />
</div>
```

app.module.ts

```js
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { FormsModule } from '@angular/forms';

import { AppComponent } from './app.component';
import { EmployeeComponentComponent } from './employee-component/employee-component.component';
import { ConvertToSpacesPipe } from './shared/convert-to-spaces.pipe';

@NgModule({
  imports: [BrowserModule, FormsModule],
  declarations: [AppComponent, EmployeeComponentComponent, ConvertToSpacesPipe],
  bootstrap: [AppComponent]
})
export class AppModule {}

```

app.component.html

```html
<app-employee-component></app-employee-component>
```


