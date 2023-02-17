{% include navbar.html %}

<style>
@import url(https://fonts.googleapis.com/css?family=Lato:400,700);
$green: #86BB71;
$blue: #94C2ED;
$orange: #E38968;
$gray: #92959E;
*, *:before, *:after {
  box-sizing: border-box;
}
body {
  background: #C5DDEB;
  font: 14px/20px "Lato", Arial, sans-serif;
  padding: 40px 0;
  color: white;
}
.container {
  margin: 0 auto;
  width: 750px;
  background: #444753;
  border-radius: 5px;
}
.people-list {
  width:260px;
  float: left;
  .search {
    padding: 20px;
  }
  input {
    border-radius: 3px;
    border: none;
    padding: 14px;
    color: white;
    background: #6A6C75;
    width: 90%;
    font-size: 14px;
  }
  .fa-search {
    position: relative;
    left: -25px;
  }
  ul {
    padding: 20px;
    height: 770px;
    li {
      padding-bottom: 20px;
    }
  }
  img {
    float: left;
  }
  .about {
    float: left;
    margin-top: 8px;
  }
  .about {
    padding-left: 8px;
  }
  .status {
    color: $gray;
  }
}
.chat {
  width: 490px;
  float:left;
  background: #F2F5F8;
  border-top-right-radius: 5px;
  border-bottom-right-radius: 5px;
  color: #434651;
  .chat-header {
    padding: 20px;
    border-bottom: 2px solid white;
    img {
      float: left;
    }
    .chat-about {
      float: left;
      padding-left: 10px;
      margin-top: 6px;
    }
    .chat-with {
      font-weight: bold;
      font-size: 16px;
    }
    .chat-num-messages {
      color: $gray;
    }
    .fa-star {
      float: right;
      color: #D8DADF;
      font-size: 20px;
      margin-top: 12px;
    }
  }
  .chat-history {
    padding: 30px 30px 20px;
    border-bottom: 2px solid white;
    overflow-y: scroll;
    height: 575px;
    .message-data {
      margin-bottom: 15px;
    }
    .message-data-time {
      color: lighten($gray, 8%);
      padding-left: 6px;
    }
    .message {
      color: white;
      padding: 18px 20px;
      line-height: 26px;
      font-size: 16px;
      border-radius: 7px;
      margin-bottom: 30px;
      width: 90%;
      position: relative;
      &:after {
        bottom: 100%;
        left: 7%;
        border: solid transparent;
        content: " ";
        height: 0;
        width: 0;
        position: absolute;
        pointer-events: none;
        border-bottom-color: $green;
        border-width: 10px;
        margin-left: -10px;
      }
    }
    .my-message {
      background: $green;
    }
    .other-message {
      background: $blue;
      &:after {
        border-bottom-color: $blue;
        left: 93%;
      }
    }
  }
  .chat-message {
    padding: 30px;
    textarea {
      width: 100%;
      border: none;
      padding: 10px 20px;
      font: 14px/22px "Lato", Arial, sans-serif;
      margin-bottom: 10px;
      border-radius: 5px;
      resize: none;
    }
    .fa-file-o, .fa-file-image-o {
      font-size: 16px;
      color: gray;
      cursor: pointer;
    }
    button {
      float: right;
      color: $blue;
      font-size: 16px;
      text-transform: uppercase;
      border: none;
      cursor: pointer;
      font-weight: bold;
      background: #F2F5F8;
      &:hover {
        color: darken($blue, 7%);
      }
    }
  }
}
.online, .offline, .me {
    margin-right: 3px;
    font-size: 10px;
  }
.online {
  color: $green;
}
.offline {
  color: $orange;
}
.me {
  color: $blue;
}
.align-left {
  text-align: left;
}
.align-right {
  text-align: right;
}
.float-right {
  float: right;
}
.clearfix:after {
	visibility: hidden;
	display: block;
	font-size: 0;
	content: " ";
	clear: both;
	height: 0;
}
</style>

<script>
(function(){
  var chat = {
    messageToSend: '',
    messageResponses: [
      'Why did the web developer leave the restaurant? Because of the table layout.',
      'How do you comfort a JavaScript bug? You console it.',
      'An SQL query enters a bar, approaches two tables and asks: "May I join you?"',
      'What is the most used language in programming? Profanity.',
      'What is the object-oriented way to become wealthy? Inheritance.',
      'An SEO expert walks into a bar, bars, pub, tavern, public house, Irish pub, drinks, beer, alcohol'
    ],
    init: function() {
      this.cacheDOM();
      this.bindEvents();
      this.render();
    },
    cacheDOM: function() {
      this.$chatHistory = $('.chat-history');
      this.$button = $('button');
      this.$textarea = $('#message-to-send');
      this.$chatHistoryList =  this.$chatHistory.find('ul');
    },
    bindEvents: function() {
      this.$button.on('click', this.addMessage.bind(this));
      this.$textarea.on('keyup', this.addMessageEnter.bind(this));
    },
    render: function() {
      this.scrollToBottom();
      if (this.messageToSend.trim() !== '') {
        var template = Handlebars.compile( $("#message-template").html());
        var context = {
          messageOutput: this.messageToSend,
          time: this.getCurrentTime()
        };
        this.$chatHistoryList.append(template(context));
        this.scrollToBottom();
        this.$textarea.val('');
        // responses
        var templateResponse = Handlebars.compile( $("#message-response-template").html());
        var contextResponse = {
          response: this.getRandomItem(this.messageResponses),
          time: this.getCurrentTime()
        };
        setTimeout(function() {
          this.$chatHistoryList.append(templateResponse(contextResponse));
          this.scrollToBottom();
        }.bind(this), 1500);
      }
    },
    addMessage: function() {
      this.messageToSend = this.$textarea.val()
      this.render();
    },
    addMessageEnter: function(event) {
        // enter was pressed
        if (event.keyCode === 13) {
          this.addMessage();
        }
    },
    scrollToBottom: function() {
       this.$chatHistory.scrollTop(this.$chatHistory[0].scrollHeight);
    },
    getCurrentTime: function() {
      return new Date().toLocaleTimeString().
              replace(/([\d]+:[\d]{2})(:[\d]{2})(.*)/, "$1$3");
    },
    getRandomItem: function(arr) {
      return arr[Math.floor(Math.random()*arr.length)];
    }
  };
  chat.init();
  var searchFilter = {
    options: { valueNames: ['name'] },
    init: function() {
      var userList = new List('people-list', this.options);
      var noItems = $('<li id="no-items-found">No items found</li>');
      userList.on('updated', function(list) {
        if (list.matchingItems.length === 0) {
          $(list.list).append(noItems);
        } else {
          noItems.detach();
        }
      });
    }
  };
  searchFilter.init();
})();
</script>



<!-- <script>
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
</script> -->