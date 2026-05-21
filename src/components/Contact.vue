<script setup>
    import { ref, onMounted, onBeforeMount } from 'vue';

    import { Notyf } from 'notyf';
    import 'notyf/notyf.min.css';

    const notyf = new Notyf();

    const WEB3FORMS_ACCESS_KEY = "f2616001-c73c-4db1-91dc-1dd080faac9f";

    const subject = "New message from Portfolio Contact Form";

    const fname = ref("");
    const lname = ref("");
    const email = ref("");
    const message = ref("");

    const isLoading = ref(false);


    const submitForm = async() => {

        isLoading.value = true;

        try{
            const response = await fetch("https://api.web3forms.com/submit", {
                method: "POST",
                headers: {
                    "Content-Type": "application/json",
                    Accept: "application/json"
                },
                body: JSON.stringify({
                    access_key: WEB3FORMS_ACCESS_KEY,
                    subject: subject,
                    name: `${fname.value} ${lname.value}`,
                    email: email.value,
                    message: message.value
                })
            });

            const result = await response.json();

            if(result.success){
                console.log(result)

                isLoading.value = false;
                notyf.success("Message sent!");
            }
        } catch(error) {
            console.log(error);

            isLoading.value = false;
            notyf.error("Failed to send message");

        } finally {
            resetRecaptcha();
        }
    }

    // recaptcha integration

    const SITE_KEY = "6LeXX_UsAAAAAGZhb_7Ei0Hg4IQ8HiUC9CptBSPr";

    const recaptchaContainer = ref(null);
    const recaptchaWidgetID = ref(null);
    const recaptchaToken = ref("");

    function onRecaptchaSuccess(token) {
        recaptchaToken.value = token;
    }

    function onRecaptchaExpired(){
        recaptchaToken.value = "";
    }

    function renderRecaptcha(){
        if(!window.grecaptcha){
            console.error('reCAPTCHA not loaded');
            return;
        }

        recaptchaWidgetID.value = window.grecaptcha.render(recaptchaContainer.value, {
            sitekey: SITE_KEY,
            size: 'normal',
            callback: onRecaptchaSuccess,
            'expired-callback': onRecaptchaExpired
        })
    }

    function resetRecaptcha(){
        if(recaptchaWidgetID.value !== null) {
            window.grecaptcha.reset(recaptchaWidgetID.value);
            recaptchaToken.value = '';
        }
    }

    onMounted(() => {
        const interval = setInterval(() => {
            if(window.grecaptcha && window.grecaptcha.render) {
                renderRecaptcha();
                clearInterval(interval)
            }
        }, 100);

        onBeforeMount(() => {
            clearInterval(interval);
        })
    })

</script>

<template>
    <section id="contact" class="my-auto p-5">
        <div class="row mb-4">
            <div class="col-12">
            <h1 class="mb-4">
                Get In Touch!
            </h1>
            </div>
        </div>
        <div class="row g-3 justify-content-center px-2">
            <div class="col-12 col-lg-5 p-3 p-md-4">
                <form @submit.prevent="submitForm">
                <div class="row">
                    <div class="col-12 col-sm-6 mb-2">
                        <input type="text" v-model="fname" class="form-control form-input" id="InputFirstName" placeholder="First Name">
                    </div>
                    <div class="col-12 col-sm-6 mb-2">
                        <input type="text" v-model="lname" class="form-control form-input" id="InputLastName" placeholder="Last Name">
                    </div>
                </div>
                <div class="mb-2">
                    <input type="email" class="form-control form-input" id="exampleInputEmail1" placeholder="Email address" aria-describedby="emailHelp">
                </div>
                <div class="mb-3">
                    <textarea v-model="message" class="form-control form-input" id="Message" rows="3" placeholder="Message"></textarea>
                </div>
                <div class="d-flex justify-content-end mt-1 mb-3">
                    <div ref="recaptchaContainer"></div>
                </div>
                <button type="submit" class="btn btn-dark w-100" :disabled="isLoading || !recaptchaToken.value">{{isLoading ? "Sending..." : "Submit"}}</button>

                </form>
            </div>
            <div class="col-12 col-lg-5 p-3 p-md-4">
                <div class="mb-3">
                    <div class="contact-info bg-white p-3">
                        <span>suissacseyer@gmail.com</span>
                    </div>
                </div>
                <div class="mb-4">
                    <div class="contact-info bg-white p-3">
                        <span>Batangas, Philippines</span>
                    </div>
                </div>
                <div class="social-media-icons">
                    <div class="d-flex justify-content-center gap-2 gap-md-3 flex-wrap">
                        <a href="https://www.facebook.com/suissac.seyer" target="_blank" class="social-icon" title="Facebook">
                            <div class="social-circle">
                                <img src="https://static.vecteezy.com/system/resources/previews/018/930/698/non_2x/facebook-logo-facebook-icon-transparent-free-png.png" alt="Facebook" class="social-icon-img">
                            </div>
                        </a>
                        <a href="https://github.com/cashauce" target="_blank" class="social-icon" title="GitHub">
                            <div class="social-circle">
                                <img src="https://static.vecteezy.com/system/resources/previews/016/833/872/non_2x/github-logo-git-hub-icon-on-white-background-free-vector.jpg" alt="GitHub" class="social-icon-img">
                            </div>
                        </a>
                        <a href="https://www.linkedin.com/in/cassius-reyes-03aaaa302/" target="_blank" class="social-icon" title="LinkedIn">
                            <div class="social-circle">
                                <img src="https://static.vecteezy.com/system/resources/previews/018/930/480/non_2x/linkedin-logo-linkedin-icon-transparent-free-png.png" alt="LinkedIn" class="social-icon-img">
                            </div>
                        </a>
                        <a href="https://www.instagram.com/cashauceeee?igsh=aDB2amk3Y2Zkbm0w" target="_blank" class="social-icon" title="Instagram">
                            <div class="social-circle">
                                <img src="https://static.vecteezy.com/system/resources/previews/018/930/415/non_2x/instagram-logo-instagram-icon-transparent-free-png.png" alt="Instagram" class="social-icon-img">
                            </div>
                        </a>
                    </div>
                </div>
            </div>
        </div>
    </section>

</template>