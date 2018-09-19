<template>
  <div class="container">
    <div class="row">
      <div class="col-xs-12 col-sm-8 offset-sm-2 col-md-6 offset-md-3">
          <h1 class="text-center">The Super Quiz</h1>
      </div>

    </div>
    <hr>
    <div class="row">

      <div class="col-xs-12 col-sm-8 offset-sm-2 col-md-6 offset-md-3">
        <transition name="flip" mode="out-in">
          <div class="alert alert-danger" role="alert" v-if="wrong">
            <h1 class="text-center text-danger">
              Your answer is incorrect please try again!
            </h1>
          </div>
        </transition>
       <transition name="flip" mode="out-in">
         <component :is="mode" @answered="answered($event)" @confirmed="mode='app-question'"></component>
       </transition>
      </div>
    </div>
  </div>
</template>

<script>
  import Answer from './components/Answer'
  import Question from './components/Question'
export default {
  name: 'app',
    components:{
      appQuestion: Question,
      appAnswer:Answer,
    },
  data () {
    return {
      mode:'app-question',
        wrong:false
    }
  },
    methods:{
        answered(isCorrect)
        {
            if(isCorrect)
            {
                this.mode = 'app-answer'
                this.wrong = false
            }
            else{
                this.mode = 'app-question'
                this.wrong = true
            }
        }
    }
}
</script>

<style>
  .flip-enter {
    /*transform: rotateY(0deg);*/
  }

  .flip-enter-active {
    animation: flip-in  0.5s ease-out forwards;
  }

  .flip-leave {
    /*transform: rotateY(0deg);*/
  }

  .flip-leave-active {
    animation: flip-out 0.5s ease-out forwards;
  }

  @keyframes flip-out {
    from {
      transform: rotateY(0deg);
    }
    to {
      transform: rotateY(90deg);
    }
  }

  @keyframes flip-in {
    from {
      transform: rotateY(90deg);
    }
    to {
      transform: rotateY(0deg);
    }
  }
  /*
  .slide-enter{

  }
  .slide-enter-active{
    animation: slide-in 1s ease-out forwards;
    transition: opacity 0.5s;
  }
  .slide-leave{}
  .slide-leave-active{
    animation: slide-out 1s ease-out forwards;
    transition: opacity 1s;
    opacity: 0;
  }
  .slide-move{
    transition: transform 1s;

  }
  @keyframes slide-in {
    from{
      transform: translateY(5px);
    }
    to{
      transform: translateY(0);
    }
  }

  @keyframes slide-out {
    from{
      transform: translateY(0);
    }
    to{
      transform: translateY(5px);
    }
  }*/
</style>
