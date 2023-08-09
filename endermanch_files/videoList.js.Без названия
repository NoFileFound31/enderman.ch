(() => {
    const wrapFetch = f => f.then(resp => resp.text())
    .then(resp => {
        if (!resp.startsWith("<!--malwarewatch.org__generated-->")) {
            return;
        }

        return resp;
    });

    const fetchPromises = [
        wrapFetch(fetch("/video_list.html")),
        wrapFetch(fetch("/andrew_video_list.html"))
    ]

    const peeks = [
        document.querySelector(".enderman-peek"),
        document.querySelector(".andrew-peek")
    ];

    const videoLists = document.querySelectorAll(".container .side-panel.load-video-views .videos");

    const oldContent = videoLists[0].innerHTML;

    const switchList = (i, changePeeks = true) => {
        const otherPeekIndex = i === "1" ? "0" : "1";
        if (changePeeks) {
            const peekToReveal = peeks[otherPeekIndex];

            peekToReveal.classList.remove("peek-hidden");
            peeks[i].classList.add("peek-hidden");
        }

        for (const list of videoLists) {
            list.classList.add("has-spinner");
            list.innerHTML = oldContent;
        }

        fetchPromises[otherPeekIndex].then(text => {
            for (const list of videoLists) {
                list.classList.remove("has-spinner");
                list.innerHTML = text;
            }
        })
    }

    // return;

    for (const i in peeks) {
        peeks[i].addEventListener("click", () => switchList(i));
    }

    switchList("1", false);
})();