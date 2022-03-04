# AngularJest

## Step 1: 
`npm uninstall @types/jasmine jasmine-core karma karma-chrome-launcher`
## Step 2: 
  - Remove test object from Angular.json
## Step 3: 
  - Delete karma.conf.js file and test.ts file
## Step 4: 
  `npm i jest @types/jest jest-preset-angular`
## Step 5:
Run on root folder:
  ```bash
  npx jest --init
  ```
  - Choose from options `coverage,JSDOM,V8`
## Step 6: Create setup.jest.ts file.
  - Add `import 'jest-preset-angular/setup-jest'`
## Step 7: Update tsconfig.spec.json file
  - Add "jest" to types and "src/setup.jest.ts"
  ```json
    {
      "extends": "./tsconfig.json",
      "compilerOptions": {
        "outDir": "./out-tsc/spec",
        "types": [
          "jest",
          "node"
        ]
      },
      "files": [
        "src/setup.jest.ts",
        "src/polyfills.ts"
      ],
      "include": [
        "src/**/*.spec.ts",
        "src/**/*.d.ts"
      ]
    }
  ```
  
## Step 8: 
 - Update/Uncoment jest.config.js file with the following content:
  ```json
  "jest": {
    "preset": "jest-preset-angular",
    "setupFilesAfterEnv": [
      "<rootDir>/src/setup.jest.ts"
    ],
    "testPathIgnorePatterns": [
      "<rootDir>/node_modules/",
      "<rootDir>/dist/"
    ],
    "globals": {
      "ts-jest": {
        "tsConfig": "<rootDir>/tsconfig.spec.json",
        "stringifyContentPathRegex": "\\.html$"
      }
    }
  }
  ```
## Step 9: Add scripts in package.json to run JEST
  ```json
    {   
      ...
      "test": "jest",
      "test:watch": "jest --watch",
      "test:coverage": "jest --coverage"
        ...
    }
  ```
## Step 10: Create Test Cases
- Replace app.component.spec.ts file with the following code
```typescript
    import { AppComponent } from "./app.component"
    import { ComponentFixture, TestBed } from "@angular/core/testing";
    import { FormsModule } from "@angular/forms";
    import { AppRoutingModule } from "./app-routing.module";


    describe( 'AppComponent', () => {
      let fixture: ComponentFixture<AppComponent>;

      beforeEach(() => {
        // defin the TestBedConfiguration
        TestBed.configureTestingModule({
          declarations: [AppComponent],
          imports: [FormsModule, AppRoutingModule]
        }).compileComponents(); // the component will be compiled
                                // (includes HTML Tremplate)
      });
      beforeEach(() => {
        fixture = TestBed.createComponent(AppComponent);
      });
      it('should have a title AngularJestSetup', () => {
      expect (fixture.title).toEqual ('AngularJestSetup');
      })
      it('adds 1 + 2 to equal 3', () => {
      expect (fixture.sum(1, 2)).toBe(3);
      })
      it('should render title', () => {
          const fixture = TestBed.createComponent(AppComponent);
          fixture.detectChanges();
          const compiled = fixture.nativeElement as HTMLElement;
          expect(compiled.querySelector('.content span')?.textContent).toContain('AngularJestSetup app is running!');
        });
    }
    )
```
## Step 10: Run test cases and check coverage report
`npm run test`