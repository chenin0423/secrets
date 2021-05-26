# secrets
Learning "Authentication and Security" program in Node JS
Level 5: Cookies and Sessions

//Setup steps
//Step 1
const session = require("express-session");
const passport = require("passport");
const passportLocalMongoose = require("passport-local-mongoose");

//Step 2
app.use(session({
  secret: 'Our little secret.',
  resave: false,
  saveUninitialized: true,
}));

app.use(passport.initialize());
app.use(passport.session());

mongoose.connect("mongodb://localhost:27017/userDB", { useNewUrlParser: true, useUnifiedTopology: true, useCreateIndex: true } );

const userSchema = new mongoose.Schema( {
  email: String,
  password: String
});

//Step 3
userSchema.plugin(passportLocalMongoose);

const User = new mongoose.model("User", userSchema);
passport.use(User.createStrategy());
passport.serializeUser(User.serializeUser());
passport.deserializeUser(User.deserializeUser());
