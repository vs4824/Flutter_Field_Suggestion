# Flutter Field Suggestion

## Usage

In this example, we're using the FieldSuggestion.network widget to display suggestions for a username input field. We've provided an inputDecoration with a hint text, a future function that fetches the suggestions based on the user input, a textController that controls the text in the input field, a boxController that controls the visibility of the suggestion box, and a builder function that defines how the suggestions are displayed in the suggestion box.

Note that FieldSuggestion uses generics to allow for suggestions of different types. In the example above, we're using String as the type parameter for FieldSuggestion.network However, any other type can be used, depending on the type of suggestions being displayed.

   ```
   FieldSuggestion<String>.network(
  inputDecoration: InputDecoration(
    hintText: 'Username', // optional
  ),
  future: (input) => future.call(input),
  textController: controller,
  boxController: boxController, // optional
  builder: (context, snapshot) {
    if (snapshot.connectionState != ConnectionState.done) {
      return Center(child: CircularProgressIndicator());
    }

    final result = snapshot.data ?? [];
    return ListView.builder(
      itemCount: result.length,
      itemBuilder: (context, index) {
        return GestureDetector(
          onTap: () {
            setState(() => controller.text = result[index]);
            boxControllerNetwork.close?.call();
          },
          child: Card(child: ListTile(title: Text(result[index]))),
        );
      },
    );
  },
)
   ```
