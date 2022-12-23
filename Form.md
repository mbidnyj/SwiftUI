## Form, Group, Section
Form has up to 10 views inside, Group just solve the problem of having more than 10 elements in 1 view as well as Section(but it visually separated), it is also possible to scroll elements inside the Form

``` swift
Form {
    Section {
        Text("Hello, world!")
    }

    Group {
        Text("Hello, world!")
        Text("Hello, world!")
    }
}
```

## NavigationView
Used to group Form views and add aditional space bar at the top with blured background(that can be used for the title, so when we scroll screen, it does not overlap with clock for example)

``` swift
NavigationView {
    Form {
        Section {
            Text("Hello, world!")
        }
    }
    .navigationTitle("SwiftUI")
    .navigationBarTitleDisplayMode(.inline)
}
```

## TextField
Used to read user input

``` swift
struct ContentView: View {
    @State private var name = ""

    var body: some View {
        Form {
            TextField("Enter your name", text: $name)
            Text("Hello, world!")
        }
    }
}
```

``` swift
@FocusState private var amountIsFocused: Bool

///

TextField("Amount",
    value: $checkAmount,
    format: .currency(
    code: Locale.current.currency?.identifier ?? "USD")
    )
        .keyboardType( .decimalPad)
        .focused($amountIsFocused)
```

## ForEach
Used to loop through ranges or arrays and are used inside Form elements to enable scrolling

``` swift
struct ContentView: View {
    let students = ["Harry", "Hermione", "Ron"]
    @State private var selectedStudent = "Harry"

    var body: some View {
        NavigationView {
            Form {
                Picker("Select your student", selection: $selectedStudent) {
                    ForEach(students, id: \.self) {
                        Text($0)
                    }
                }
            }
        }
    }
}
```

## Picker
Used to choose one of the options available. When ForEach loop is used inside, not the value inside the loop in transmitted but the index
``` swift
Section {
    TextField("Amount", value: $checkAmount, format: .currency(
    code: Locale.current.currency?.identifier ?? "USD")
    )
        .keyboardType(.decimalPad)

    Picker("Number of people", selection: $numberOfPeople) {
        ForEach(2 ..< 100) {
            Text("\($0) people")
        }
    }
        .pickerStyle(.segmented)
}
```

``` swift
Section {
    Picker("Tip percentage", selection: $tipPercentage) {
        ForEach(tipPercentages, id: \.self) {
            Text($0, format: .percent)
        }
    }
    .pickerStyle(.segmented)
} header: {
    Text("How much tip do you want to leave?")
}
```

## ToolbarItemGroup
Used inside of NavigationView to place additional items in specified places
``` swift
.toolbar {
    ToolbarItemGroup(placement: .keyboard) {           
        Spacer()

        Button("Done") {
            amountIsFocused = false
        }
    }
}
```