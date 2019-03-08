# react-style-guide

- redux file separation
    - create redux parts such as actions, actionTypes, and reducers in the redux/modules folder
        - initially, it could be a single nameOfModule.js file (i.e. redux/modules/nameOfModule.js)
        - as the module grows, separate into separate files i.e.:
            - add-user.actions.js
            - add-user.actionTypes.js
            - add-user.reducer.js
    - reasons (from Google's style guide used for large scale applications):
        - Do define one thing, such as a service or component (or in our case, actions, reducers), per file.
        - Consider limiting files to 400 lines of code.
        - Why? One component per file makes it far easier to read, maintain, and avoid collisions with teams in source control.
        - Why? One component per file avoids hidden bugs that often arise when combining components in a file where they may share variables, create unwanted closures, or unwanted coupling with dependencies.
        - Why? A single component can be the default export for its file which facilitates lazy loading with the router.
        - The key is to make the code more reusable, easier to read, and less mistake prone.
        - [Reference: Single Responsibility Principle link](https://angular.io/guide/styleguide#single-responsibility)
- To Be Discussed
    - do not pass the destructured `this.props` unnecessarily
        - causes unnecessary re renders when a property of the props changes that is not even used in the child component
    - not necessary to destructure in the mapStateToProps
        - state changes occur in the reducer, and should NOT happen at the component level.
        - Therefore, it does not need to be descructured for shallow copying purposes. Adds unnecessary clutter, and possibly open doors for antipattern
    - always use triple equals for consistent checking behavior in JS
    - folder structure
        - redux: components (presentational) vs containers
            - components ARE NOT connected to redux while containers ARE
            - [Dan Abramov's acticle discussing the differences](https://medium.com/@dan_abramov/smart-and-dumb-components-7ca2f9a7c7d0)
    - propTypes
        - reasons:
            - better experience debugging, 
            - enables intellisense
        - how to:
            - add properties to the class instead of using static methods
                - visually seeing the proptypes separately from the class is easier to digest
            - when using HOCs ie. withStyles or connect, declare a variable for the output component instead of exporting it directly. Currently the extension [React PropTypes Intellisense](https://marketplace.visualstudio.com/items?itemName=OfHumanBondage.react-proptypes-intellisense) only supports this method.
                - note to self: alternative method
                  /**
                   * @augments {Component<{x: string, y: number, store: store}, {}>}
                   */
