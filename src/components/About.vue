<template>
    <section id="about" class="my-3 p-5">

        <!-- Heading Row -->
        <div class="row">
            <div class="col-md-6">
            <h1 class="d-inline-block mb-4">
                About Me
            </h1>
            </div>
        </div>

        <!-- Content Row -->
        <div class="row gx-5 align-items-start">
        <!-- Left: Photo Col -->
            <div class="col-12 col-md-6 mb-4 mb-md-0">
                <div class="border border-dark ratio ratio-1x1 bg-light d-flex align-items-center justify-content-center">
                    <img src="/images/about_me.jpg" alt="Profile Picture" class="img-fluid img-placeholder" width="400" height="400">
                </div>
            </div>
        <!-- Right: Text & Achievements Column -->
            <div class="col-12 col-md-6">
                <!-- Bio Box 1 -->
                <div id="bio-1" class="bio px-2 mb-4 text-center">
                    <p>
                        Computer Science graduate with international backgrounds that spans the Philippines and Saudi Arabia. Now focused on contributing in the tech industry.
                    </p>
                </div>

                <!-- Bio Box 2 -->
                <div id="bio-2" class="bio px-2 mb-4 text-center">
                    <p>
                        Full-Stack Developer with a strong foundation in both front-end and back-end technologies.
                    </p>
                </div>

                <!-- Achievements Accordion -->
                <div class="accordion" id="achievementsAccordion">
                    <div class="accordion-item">
                        <h2 class="accordion-header">
                            <button class="accordion-button" type="button" data-bs-toggle="collapse" data-bs-target="#achievement1" aria-expanded="true" aria-controls="BS in Computer Science">
                                Bachelor of Science in Computer Science (2022)
                            </button>
                        </h2>
                        <div id="achievement1" class="accordion-collapse collapse" data-bs-parent="#achievementsAccordion">
                            <div class="accordion-body">
                                <p>Batangas State University - Alangilan Campus (GWA: 1.7212)</p>
                                <hr>
                                <p><b>Thesis Title: </b>Enhanced Compression Time Efficiency of Brain MRI Fractal Image Compression using CNN-Guided and KD-Tree Optimized Encoding</p>
                            </div>
                        </div>
                    </div>
                </div>
                <!-- Personality Tags -->
                <div class="personality-tags-container">
                    <div class="personality-tag">Gamer</div>
                    <div class="personality-tag">Curious</div>
                    <div class="personality-tag">Collaborative</div>
                    <div class="personality-tag">Coffee Fueled</div>
                </div>
            </div>
        </div>
    </section>
</template>