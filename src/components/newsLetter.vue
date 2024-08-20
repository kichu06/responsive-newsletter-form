<template>

    <div class="container" v-if="isVisible">
      <form class="form-container" @submit.prevent="handleSubscribe(email)" novalidate>
        <div class="content">
          <h1>Stay updated!</h1>
          <p>Join 60,000+ Product Managers Receiving Monthly Updates on:</p>
          <ul class="custom-bullets">
            <li><p>Product discovery and building what matters</p></li>
            <li><p>Measuring to ensure updates are a success</p></li>
            <li><p>And much more!</p></li>
          </ul>
          <div class="email-group">
          <label for="email">Email address</label>
          <p v-if="errorMessage" class="error-message">{{ errorMessage }}</p>
        </div>
          <input type="email" placeholder="email@company.com"  v-model="email"   :class="{ invalid: errorMessage }"/> 
         
          <button  type="submit">Subscribe to monthly newsletter</button>
        </div>
        <div class="image-container">
          <img
            :src="require(`@/assets/images/illustration-sign-up-${isDesktop ? 'desktop' : 'mobile'}.svg`)"
            :alt="'Newsletter logo'"
       
          />
        </div>
      </form>
    </div>
    <div class="container" v-else>
      <div class="confirm-container" >
        <div class="success-img-container"><img src="../assets/images/icon-success.svg" alt="success logo"/></div>
        
        <h1>Thank you for subscribing!</h1>
        <p> A confirmation email has been sent to ash@loremcompany.com. Please open it and click the button inside to confirm your subscription.</p>
         <button @click="handleDismiss">Dismiss message</button>
      
        </div>
      
    </div>
</template>

<script>
export default {
   name: 'newsLetter',
  data() {
    return {
      isDesktop: true,
      isVisible:true,
      email:'',
     errorMessage: ''
    };
  },
  methods: { 
   
      handleSubscribe() {
                    const emailPattern = /^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/;
                    if (emailPattern.test(this.email)) {
                        console.log('E-mail submitted');
                        this.isVisible = false;
                        this.errorMessage = '';
                    } else {
                        this.errorMessage = 'valid email required.';
                        console.log(this.errorMessage);
                    }
                },
    handleResize() {
      this.isDesktop = window.innerWidth > 598;
    },
    handleDismiss(){
         window.location.reload();
    }
  },
  mounted() {
    this.handleResize(); 
    window.addEventListener('resize', this.handleResize); 
  },
  beforeUnmount() {
    window.removeEventListener('resize', this.handleResize);
  }
};
</script>



<style lang="scss">
 @import '../assets/newsletter.scss';
 @import '../assets/confirm.scss'
</style>
