<script>
    let imageUrl = ""
    let isLoading = false

    async function handleUpload(event) {
        isLoading = true
        const file = event.target.files[0];
        const formData = new FormData();
        formData.append('file', file);

        // 파일 업로드 처리
        const fileName = new Date().getTime().toString(36);
        const response = await fetch(`http://api.rumor-lab.com/cartoon?fileName=${fileName}`, {
            method: 'POST',
            body: formData
        })

        const jsonData = await response.json()
        imageUrl = "http://api.rumor-lab.com" + jsonData.cartoonImagePath
        document.querySelector(".svelte-card").style.backgroundImage = `url(${imageUrl})`

        const reader = new FileReader();
        reader.onload = () => {
            // reader.result;
        };
        reader.readAsDataURL(file);
    }
</script>


<div class="grid place-items-center mt-10">
    <div class="text-4xl font-bold text-center"> Convert Photo to Cartoon<br>in Seconds</div>
    <div class="w-96 mt-11 bg-white rounded-lg shadow-lg bg-center bg-cover">
        <label for="dropzone-file"
               class="flex flex-col items-center justify-center w-full h-64 border-2 border-gray-300 border-dashed rounded-lg cursor-pointer bg-gray-50 dark:hover:bg-bray-800 dark:bg-gray-700 hover:bg-gray-100 dark:border-gray-600 dark:hover:border-gray-500 dark:hover:bg-gray-600">
            <div class="flex flex-col items-center justify-center pt-5 pb-6">
                <svg aria-hidden="true" class="w-10 h-10 mb-3 text-gray-400" fill="none" stroke="currentColor"
                     viewBox="0 0 24 24" xmlns="http://www.w3.org/2000/svg">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                          d="M7 16a4 4 0 01-.88-7.903A5 5 0 1115.9 6L16 6a5 5 0 011 9.9M15 13l-3-3m0 0l-3 3m3-3v12"></path>
                </svg>
                <p class="mb-2 text-sm text-gray-500 dark:text-gray-400"><span
                        class="font-semibold">Click to upload</span> or drag and drop</p>
                <p class="text-xs text-gray-500 dark:text-gray-400">SVG, PNG, JPG or GIF (MAX. 800x400px)</p>
            </div>
            <input id="dropzone-file" type="file" class="hidden" on:change={handleUpload}/>
        </label>
    </div>

    <div class="mt-10">
        <div class="text-center mb-10">
            <button disabled type="button" class:hidden={!isLoading}
                    class="py-2.5 px-5 mr-2  text-sm font-medium text-gray-900 bg-white rounded-lg border border-gray-200 hover:bg-gray-100 hover:text-blue-700 focus:z-10 focus:ring-2 focus:ring-blue-700 focus:text-blue-700 dark:bg-gray-800 dark:text-gray-400 dark:border-gray-600 dark:hover:text-white dark:hover:bg-gray-700 inline-flex items-center">
                <svg aria-hidden="true" role="status"
                     class="inline w-4 h-4 mr-3 text-gray-200 animate-spin dark:text-gray-600" viewBox="0 0 100 101"
                     fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path d="M100 50.5908C100 78.2051 77.6142 100.591 50 100.591C22.3858 100.591 0 78.2051 0 50.5908C0 22.9766 22.3858 0.59082 50 0.59082C77.6142 0.59082 100 22.9766 100 50.5908ZM9.08144 50.5908C9.08144 73.1895 27.4013 91.5094 50 91.5094C72.5987 91.5094 90.9186 73.1895 90.9186 50.5908C90.9186 27.9921 72.5987 9.67226 50 9.67226C27.4013 9.67226 9.08144 27.9921 9.08144 50.5908Z"
                          fill="currentColor"/>
                    <path d="M93.9676 39.0409C96.393 38.4038 97.8624 35.9116 97.0079 33.5539C95.2932 28.8227 92.871 24.3692 89.8167 20.348C85.8452 15.1192 80.8826 10.7238 75.2124 7.41289C69.5422 4.10194 63.2754 1.94025 56.7698 1.05124C51.7666 0.367541 46.6976 0.446843 41.7345 1.27873C39.2613 1.69328 37.813 4.19778 38.4501 6.62326C39.0873 9.04874 41.5694 10.4717 44.0505 10.1071C47.8511 9.54855 51.7191 9.52689 55.5402 10.0491C60.8642 10.7766 65.9928 12.5457 70.6331 15.2552C75.2735 17.9648 79.3347 21.5619 82.5849 25.841C84.9175 28.9121 86.7997 32.2913 88.1811 35.8758C89.083 38.2158 91.5421 39.6781 93.9676 39.0409Z"
                          fill="#1C64F2"/>
                </svg>
                Loading...
            </button>
        </div>

        <div class="social inline-flex">
            <div class="mx-2">
                <button
                        type="button"
                        data-te-ripple-init
                        data-te-ripple-color="light"
                        class="mb-2 inline-block rounded px-6 py-2.5 text-xs font-medium uppercase leading-normal text-white shadow-md transition duration-150 ease-in-out hover:shadow-lg focus:shadow-lg focus:outline-none focus:ring-0 active:shadow-lg"
                        style="background-color: #c13584">
                    <svg
                            xmlns="http://www.w3.org/2000/svg"
                            class="h-4 w-4"
                            fill="currentColor"
                            viewBox="0 0 24 24">
                        <path
                                d="M12 2.163c3.204 0 3.584.012 4.85.07 3.252.148 4.771 1.691 4.919 4.919.058 1.265.069 1.645.069 4.849 0 3.205-.012 3.584-.069 4.849-.149 3.225-1.664 4.771-4.919 4.919-1.266.058-1.644.07-4.85.07-3.204 0-3.584-.012-4.849-.07-3.26-.149-4.771-1.699-4.919-4.92-.058-1.265-.07-1.644-.07-4.849 0-3.204.013-3.583.07-4.849.149-3.227 1.664-4.771 4.919-4.919 1.266-.057 1.645-.069 4.849-.069zm0-2.163c-3.259 0-3.667.014-4.947.072-4.358.2-6.78 2.618-6.98 6.98-.059 1.281-.073 1.689-.073 4.948 0 3.259.014 3.668.072 4.948.2 4.358 2.618 6.78 6.98 6.98 1.281.058 1.689.072 4.948.072 3.259 0 3.668-.014 4.948-.072 4.354-.2 6.782-2.618 6.979-6.98.059-1.28.073-1.689.073-4.948 0-3.259-.014-3.667-.072-4.947-.196-4.354-2.617-6.78-6.979-6.98-1.281-.059-1.69-.073-4.949-.073zm0 5.838c-3.403 0-6.162 2.759-6.162 6.162s2.759 6.163 6.162 6.163 6.162-2.759 6.162-6.163c0-3.403-2.759-6.162-6.162-6.162zm0 10.162c-2.209 0-4-1.79-4-4 0-2.209 1.791-4 4-4s4 1.791 4 4c0 2.21-1.791 4-4 4zm6.406-11.845c-.796 0-1.441.645-1.441 1.44s.645 1.44 1.441 1.44c.795 0 1.439-.645 1.439-1.44s-.644-1.44-1.439-1.44z"/>
                    </svg>
                </button>
            </div>
            <div class="mx-2">
                <button
                        type="button"
                        data-te-ripple-init
                        data-te-ripple-color="light"
                        class="mb-2 inline-block rounded px-6 py-2.5 text-xs font-medium uppercase leading-normal text-white shadow-md transition duration-150 ease-in-out hover:shadow-lg focus:shadow-lg focus:outline-none focus:ring-0 active:shadow-lg"
                        style="background-color: #1da1f2">
                    <svg
                            xmlns="http://www.w3.org/2000/svg"
                            class="h-4 w-4"
                            fill="currentColor"
                            viewBox="0 0 24 24">
                        <path
                                d="M24 4.557c-.883.392-1.832.656-2.828.775 1.017-.609 1.798-1.574 2.165-2.724-.951.564-2.005.974-3.127 1.195-.897-.957-2.178-1.555-3.594-1.555-3.179 0-5.515 2.966-4.797 6.045-4.091-.205-7.719-2.165-10.148-5.144-1.29 2.213-.669 5.108 1.523 6.574-.806-.026-1.566-.247-2.229-.616-.054 2.281 1.581 4.415 3.949 4.89-.693.188-1.452.232-2.224.084.626 1.956 2.444 3.379 4.6 3.419-2.07 1.623-4.678 2.348-7.29 2.04 2.179 1.397 4.768 2.212 7.548 2.212 9.142 0 14.307-7.721 13.995-14.646.962-.695 1.797-1.562 2.457-2.549z"/>
                    </svg>
                </button>
            </div>

            <div class="mx-2">
                <button
                        type="button"
                        data-te-ripple-init
                        data-te-ripple-color="light"
                        class="mb-2 inline-block rounded px-6 py-2.5 text-xs font-medium uppercase leading-normal text-white shadow-md transition duration-150 ease-in-out hover:shadow-lg focus:shadow-lg focus:outline-none focus:ring-0 active:shadow-lg"
                        style="background-color: #1877f2">
                    <svg
                            xmlns="http://www.w3.org/2000/svg"
                            class="h-4 w-4"
                            fill="currentColor"
                            viewBox="0 0 24 24">
                        <path
                                d="M9 8h-3v4h3v12h5v-12h3.642l.358-4h-4v-1.667c0-.955.192-1.333 1.115-1.333h2.885v-5h-3.808c-3.596 0-5.192 1.583-5.192 4.615v3.385z"/>
                    </svg>
                </button>
            </div>
            <div class="mx-2">
                <button
                        type="button"
                        data-te-ripple-init
                        data-te-ripple-color="light"
                        class="mb-2 inline-block rounded px-6 py-2.5 text-xs font-medium uppercase leading-normal text-white shadow-md transition duration-150 ease-in-out hover:shadow-lg focus:shadow-lg focus:outline-none focus:ring-0 active:shadow-lg"
                        style="background-color: #FFEB3B">
                    <img class="w-4 h-4" src="https://upload.wikimedia.org/wikipedia/commons/thumb/e/e3/KakaoTalk_logo.svg/600px-KakaoTalk_logo.svg.png?20190617212005"/>
                </button>
            </div>


            <div class="mx-2">
                <button type="button" class="relative w-[52px] h-[52px] text-gray-500 bg-white rounded-lg border border-gray-200 dark:border-gray-600 hover:text-gray-900 shadow-sm dark:hover:text-white dark:text-gray-400 hover:bg-gray-50 dark:bg-gray-700 dark:hover:bg-gray-600 focus:ring-4 focus:ring-gray-300 focus:outline-none dark:focus:ring-gray-400">
                    <svg aria-hidden="true" class="w-6 h-6 mx-auto mt-px" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path clip-rule="evenodd" d="M4 4a2 2 0 00-2 2v8a2 2 0 002 2h12a2 2 0 002-2V8a2 2 0 00-2-2h-5L9 4H4zm7 5a1 1 0 00-2 0v1.586l-.293-.293a.999.999 0 10-1.414 1.414l2 2a.999.999 0 001.414 0l2-2a.999.999 0 10-1.414-1.414l-.293.293V9z" fill-rule="evenodd"></path></svg>
                    <span class="absolute block mb-px text-sm font-medium -translate-y-1/2 -left-14 top-1/2"></span>
                </button>
            </div>
            <button type="button" class="relative w-[52px] h-[52px] text-gray-500 bg-white rounded-lg border border-gray-200 dark:border-gray-600 hover:text-gray-900 shadow-sm dark:hover:text-white dark:text-gray-400 hover:bg-gray-50 dark:bg-gray-700 dark:hover:bg-gray-600 focus:ring-4 focus:ring-gray-300 focus:outline-none dark:focus:ring-gray-400">
                <svg aria-hidden="true" class="w-6 h-6 mx-auto mt-px" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path d="M7 9a2 2 0 012-2h6a2 2 0 012 2v6a2 2 0 01-2 2H9a2 2 0 01-2-2V9z"></path><path d="M5 3a2 2 0 00-2 2v6a2 2 0 002 2V5h8a2 2 0 00-2-2H5z"></path></svg>
                <span class="absolute block mb-px text-sm font-medium -translate-y-1/2 -left-14 top-1/2"></span>
            </button>
        </div>

    </div>
</div>

<style>

    section {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        flex: 0.0;
    }

    h1 {
        width: 100%;
    }

    h3 {
        font-size: 23px;
    }

    .title {
        font-size: 30px;
        margin: 30px 0px 0px 0px;
    }

    .description {
        font-size: 20px;
        color: #85858a;
    }

    .header {
        text-align: center;
    }

    .welcome img {
        width: 100px;
        margin: 0 auto;
        display: block;
    }

    .body {
        text-align: center;
    }

    .step div {
        margin: 20px;
    }

    .upload-image {
        cursor: pointer;
        margin: 0px 50px 0px 50px;
    }


    .svelte-card {
        width: 460px;
        height: 500px;
        border-radius: 25px;
        background-color: #ffffff;
        box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
        margin: 0 auto;
        margin-bottom: 20px;
        background-size: cover;
        display: flex;
        flex-direction: column;
        justify-content: center;
    }

    .svelte-card-text {
        margin: 12px;
        font-size: 15px;
        line-height: 23px;;
    }

    .upload-limit-text {
        color: #9e9e9e;
    }

    .loading-bar {
        margin: 0 auto;
    }

    .icon-container {
        display: inline-block;
    }

    .alert-container {
        position: fixed;
        margin: 0 auto;
        left: 0;
        right: 0;
        WIDTH: 50%;
        top: 25%;
    }

    @media (max-width: 440px) {
        .svelte-card {
            width: 320px;
            height: 360px;
            margin: 0 auto;
            margin-top: 25px;
        }

    }


</style>
