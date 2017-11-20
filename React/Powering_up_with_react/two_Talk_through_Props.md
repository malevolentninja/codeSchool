# Level 2: Talk Through Props

Make components communicate by passing arguments, which are known as props in React.

### 2.3 Declaring new components I

The pattern we follow when declaring new components usually includes: 
declaring a new Class and making it extend React.Component

### 2.4 Declaring New Components II

Every component must include a method called: 
Render and return some JSX markup code.


### 2.5  converting html mockups

- In the components.js file, declare a new React component named Comment.
- Add a render() method to the Comment component.
-Copy the existing mockup from mockup.html into the render() method and return it. Remember to rename the class HTML attributes to className in JSX.

component.js
```sh
class Comment extends React.Component {
    render() {
        return(
          <div className="comment">
  <p className="comment-header">Anne Droid</p>
  <p className="comment-body">
    I wanna know what love is...
  </p>
  <div className="comment-actions">
    <a href="#">Delete comment</a>
  </div>
</div>
        );
    }
}
```

### 2.6 Reading Props

- Replace the hard-coded text within the <p> tag that has the class comment-header to read in the author prop instead.
- Now let's replace the hard-coded text within the <p> tag that has the class comment-body to read in the body prop.
```sh
class Comment extends React.Component {
  render() {
    return(
      <div className="comment">
        <p className="comment-header">
          {this.props.author}
        </p>
        <p className="comment-body">
          {this.props.body}
        </p>
        <div className="comment-actions">
          <a href="#">Delete comment</a>
        </div>
      </div>
    );
  }
}
```

### 2.7 Using the comment component


- Within the <div> element with class name comment-list, add a new Comment component.
- Provide an author prop of "Anne Droid" and a body prop of "I want to know what love is..." to the new Comment component.

```sh
class CommentBox extends React.Component {
  render() {
    return(
      <div className="comment-box">
        <h3>Comments</h3>
        <h4 className="comment-count">2 comments</h4>
        <div className="comment-list">
         <Comment
            author="Anne Droid" body="I want to know what love is..." />
        </div>
      </div>
    );
  }
}

```

### 2.9 Syntac for Using Dynamic Props
What is the correct syntax to pass the comment.author object property as a prop to the Comment component?
```sh
<Comment author={comment.author} />
```


### 2.10  Mapping components
- Add an avatarUrl property to each element in the commentList array and set the values to 'images/default-avatar.png'.
- Let's make _getComments() return an array of Comment components by calling the map() method of commentList and having it return a Comment for each item in the array.
- Now let's pass these properties as props to each Comment component: author, body, and avatarUrl. Don't forget that the callback to map takes an argument that represents each element from the calling object.
- Our console is showing a warning because we're not passing a key prop with a unique identifier for each comment in the array. Let's add a key prop to each Comment component and use comment.id as the unique identifier.

```sh
class CommentBox extends React.Component {
  render() {
    const comments = this._getComments() || [];
    return(
      <div className="comment-box">
        <h3>Comments</h3>
        <h4 className="comment-count">{comments.length} comments</h4>
        <div className="comment-list">
          {comments}
        </div>
      </div>
    );
  }

  _getComments() {
    const commentList = [
      { id: 1, author: 'Clu', body: 'Just say no to love!', avatarUrl: 'images/default-avatar.png' },
      { id: 2, author: 'Anne Droid', body: 'I wanna know what love is...', avatarUrl: 'images/default-avatar.png' }
    ];

    return commentList.map((comment) => {
      return (<Comment
               author={comment.author}
               body={comment.body}
               avatarUrl={comment.avatarUrl}
               key={comment.id} />);
    });
  }
}


class Comment extends React.Component {
  render() {
    return(
      <div className="comment">
        <p className="comment-header">
          {this.props.author}
        </p>
        <p className="comment-body">
          {this.props.body}
        </p>
        <div className="comment-actions">
          <a href="#">Delete comment</a>
        </div>
      </div>
    );
  }
}
```

### 2.11 Adding a comment Avatar


- Add an <img /> as the very first tag inside the <div> element with class comment. Reminder: All opening tags <img> without a closing tag must use the self-closing syntax <img /> instead.
- Now let's add a src attribute to our newly created <img /> tag and give it the avatarUrl prop.
- It's recommended that every <img /> tag on our page has an alt attribute. So let's add an alt attribute to our image with the following format:   `${this.props.author}'s picture`

component.js
```sh
class CommentBox extends React.Component {

  render() {
    const comments = this._getComments() || [];
    return(
      <div className="comment-box">
        <h3>Comments</h3>
        <h4 className="comment-count">{comments.length} comments</h4>
        <div className="comment-list">
          {comments}
        </div>
      </div>
    );
  }

  _getComments() {

    const commentList = [
      { id: 1, author: 'Clu', body: 'Just say no to love!', avatarUrl: 'images/default-avatar.png' },
      { id: 2, author: 'Anne Droid', body: 'I wanna know what love is...', avatarUrl: 'images/default-avatar.png' }
    ];

    return commentList.map((comment) => {
      return (<Comment
               author={comment.author}
               body={comment.body}
               avatarUrl={comment.avatarUrl}
               key={comment.id} />);
    });

  }
}

class Comment extends React.Component {
  render() {
    return(
      <div className="comment">
        <img src={this.props.avatarUrl} alt={`${this.props.author}'s picture`} />
        <p className="comment-header">{this.props.author}</p>
        <p className="comment-body">
          {this.props.body}
        </p>
        <div className="comment-actions">
          <a href="#">Delete comment</a>
        </div>
      </div>
    );
  }
}
```


### 2.12 Comment Popularity

- Make _getPopularMessage() return the following div if the value of the commentCount argument is greater than POPULAR_COUNT:
```sh
<div>
  This post is getting really popular, don't miss out!
</div>
```
- Now let's call the _getPopularMessage() method from render() right after the 
```sh <h3> ``` tag, and pass the length of comments as the argument.


component.js
```sh
class CommentBox extends React.Component {
  render() {
    const comments = this._getComments() || [];
    return(
      <div className="comment-box">
        <h3>Comments</h3>
        {this._getPopularMessage(comments.length)}
        <h4 className="comment-count">{this._getCommentsTitle(comments.length)}</h4>
        <div className="comment-list">
          {comments}
        </div>
      </div>
    );
  }

  _getPopularMessage(commentCount) {
    const POPULAR_COUNT = 10;
    if (commentCount > POPULAR_COUNT) {
       return (
         <div>
           This post is getting really popular, don't miss out!
         </div>
       );
    }
  }
  
  _getComments() {
    const commentList = [
      { id: 1, author: 'Clu', body: 'Just say no to love!', avatarUrl: 'images/default-avatar.png' },
      { id: 2, author: 'Anne Droid', body: 'I wanna know what love is...', avatarUrl: 'images/default-avatar.png' }
    ];

    return commentList.map((comment) => {
      return (<Comment
               author={comment.author}
               body={comment.body}
               avatarUrl={comment.avatarUrl}
               key={comment.id} />);
    });
  }

  _getCommentsTitle(commentCount) {
    if (commentCount === 0) {
      return 'No comments yet';
    } else if (commentCount === 1) {
      return '1 comment';
    } else {
      return `${commentCount} comments`;
    }
  }
}

class Comment extends React.Component {
  render() {
    return(
      <div className="comment">
        
        <img src={this.props.avatarUrl} alt={`${this.props.author}'s picture`} />

        <p className="comment-header">{this.props.author}</p>
        <p className="comment-body">
          {this.props.body}
        </p>
        <div className="comment-actions">
          <a href="#">Delete comment</a>
        </div>
      </div>
    );
  }
}
```
