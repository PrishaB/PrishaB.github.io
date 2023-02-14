{% include navbar.html %}

<style>
@use postcss-preset-env {
  stage: 0;
}
body {
  background-color: #E9EBEE;
  color: #1D2129;
}
#app {
  background-color: #fff;
  font-family: helvetica;
  margin: 30px auto;
  width: 500px;
  border: 1px solid;
  border-color: #E5E6E9 #DFE0E4 #D0D1D5;
  border-radius: 3px;
}
.creator {
  position: relative;
  img {
    width: 40px;
    height: 40px;
    background-size: cover;
    background-position: center;
    margin: 12px 0 0 12px;
    position: absolute;
  }
  div {
    display: inline-block;
    margin-left: 60px;
    p {
      font-size: 14px;
      &:first-of-type {
        &:hover {
          text-decoration: underline;
        }
        cursor: pointer;
        font-weight: bold;
        color: #365899;
      }
      &:last-of-type {
        font-size: 12px;
        color: #90949C;
        margin-top: -10px;
      }
    }
  }
}
.message {
  font-size: 14px;
  margin-top: 8px;
  padding: 0 12px;
  line-height: 18px;
}
.bar {
  width: calc(100% - 24px);
  border-top: 1px solid #E5E5E5;
  margin: 0 12px;
  .action-button {
    margin-left: 20px;
    display: inline-block;
    font-size: 12px;
    font-weight: bold;
    color: #7F7F7F;
    cursor: pointer;
    &:before {
      content: '';
      display: inline-block;
      height: 14px;
      margin: 0 6px -3px 0;
      width: 14px;
      background-repeat: no-repeat;
      background-size: auto;
    }
    &:first-of-type {
      margin: 0;
      &:before {
        content: '';
        background-position: -47px -164px
      }
    }
    &:nth-of-type(2) {
      &:before {
        background-position: -32px -164px;
      }
    }
    &:nth-of-type(3) {
      &:before {
         background-position: -45px -181px;
      }
    }
    &:hover {
      text-decoration: underline;
    }
  }
}
.single-comment {
  padding: 0 0 0 12px;
  &:first-of-type {
    border-top: 1px solid #E1E2E3;
    padding-top: 12px;
  }
  &:nth-of-type(2) {
    img {
    }
  }
  margin: 0;
  img {
    position: absolute;
    width: 32px;
    height: 32px;
    background-size: cover;
    background-position: center;
    border: none;
  }
  .single-container {
    padding-left: 40px;
    padding-right: 20px;
    span {
      font-size: 12px;
      margin-left: 5px;
      &:first-of-type {
        cursor: pointer;
        font-weight: bold;
        color: #365899;
        font-size: 12px;
        margin: 0;
        &:hover{
          text-decoration: underline;
        }
      }
    }
  }
  .buttons {
    margin-top: 0;
    padding-left: 40px;
    p {
      display: inline-block;
      color: #365899;
      cursor: pointer;
      text-decoration: none;
      font-size: 12px;
      margin-right: 8px;
      margin-top: 5px;
      &:hover {
        text-decoration: underline;
      }
      &:last-of-type {
        color: #90949C;
        cursor: auto;
        text-decoration: none;
      }
    }
  }
}
.comment-section {
  background-color: #F6F7F9;
  margin: 0;
}
.input {
  margin-top: 0;
  background-color: #F6F7F9;
  padding: 4px 12px 8px 12px;
  img {
    width: 32px;
    height: 32px;
    background-size: cover;
    background-position: center;
    border: none;
    position: absolute;
  }
  textarea {
    background: #fff;
    border: 1px solid #BDC7D8;
    box-sizing: border-box;
    cursor: text;
    width: calc(100% - 40px);
    margin-left: 40px;
    padding: 7px;
    font-family: helvetica;
    outline: none;
    resize: none;
    overflow: hidden;
    height: 32px;
  }
}
</style>
<script>
   var appId = "app";
var main = document.createElement("DIV");
main.id = appId;
document.body.appendChild(main);
var app = document.getElementById('app');
var Hour = React.createClass({
  getDefaultProps: function() {
    return {
      time: 42
    }
  },
  render: function() {
    return (<p>{this.props.time} h</p>);
  }
})
var Creator = React.createClass({
  getDefaultProps: function() {
    return {
      name: "Linda05"
    }
  },
  render: function() {
    return (
      <div className="creator">
        <img />
        <div>
          <p>{this.props.name}</p>
          <Hour time={4} />
        </div>
      </div>
    )
  }
});
var Message = React.createClass({
  render: function() {
    return (
      <p className="message">Omg it's snowing outside!</p>
    )
  }
});
var Action = React.createClass({
  render: function() {
    return (
      <p className="action-button" >{this.props.text}</p>
    );
  }
})
var Bar = React.createClass({
  render: function() {
    return (
      <div className="bar">
        <Action text={"Comment"} />
      </div>
    )
  }
});
var Comment = React.createClass({
  getDefaultProps: function() {
    return{name: "Douglas Adams"}
  },
  render: function() {
    return (
      <div className="single-comment">
        <img />
        <div className="single-container">
          <span>{this.props.name}</span>
          <span>{this.props.children}</span>
        </div>
        <div className="buttons">
          <Hour time={this.props.time} />
        </div>
      </div>
    );
  }
});
var CommentSection = React.createClass({
  getInitialState: function() {
    return {
      comments: []
    }
  },
  _eachComment: function(text, i) {
    return (<Comment key={i} index={i} removeComment={this._deleteComment}>{text}</Comment>)
  },
  _addComment: function(text) {
    var arr = this.state.comments
    arr.push(text);
    this.setState({comments: arr})
  },
  _handleKeyPress: function(e) {
    if (e.key === "Enter") {
      this._addComment(this.refs.newText.value);
      this.refs.newText.value = "";
      e.preventDefault();
    }
  },
  render: function() {
    return (
      <div>
        <div className="comment-section">
          <Comment name={"Linda05"} time={3}>@serafina06 I really like your picture!...</Comment>
          <Comment name={"Serafina06"} time={2}>Thank you so much!</Comment>
          {this.state.comments.map(this._eachComment)}
        </div>
        <div className="input">
          <img />
          <textarea ref="newText" onKeyPress={this._handleKeyPress} placeholder="Write a comment..."/>
        </div>
      </div>
    );
  }
});
var Post = (
  <div>
    <Creator />
    <Message />
    <Bar />
    <CommentSection />
  </div>
);
ReactDOM.render(Post, app);
// Normal js
var textarea = document.getElementsByTagName('textarea')[0];
textarea.onkeyup = function() {
  textarea.style.height = "34px";
  textarea.style.height = (textarea.scrollHeight) + "px";
}
/*  */
</script>