(ns association.facts-test
  (:require [clojure.test :refer [deftest is]]
            [association.facts :as facts]))

(deftest ama-has-spec-basis
  (let [sb (facts/spec-basis "ama")]
    (is (= 2 (count sb)))
    (is (every? #(= "8621" (:association-rule/isic %)) sb))
    (is (every? #(= "USA" (:association-rule/country %)) sb))))

(deftest unknown-association-has-no-spec-basis
  (is (nil? (facts/spec-basis "wef")))
  (is (nil? (facts/spec-basis "zzz"))))

(deftest coverage-is-honest
  (let [c (facts/coverage ["ama" "wef"])]
    (is (= 2 (:requested c)))
    (is (= 1 (:covered c)))
    (is (= ["wef"] (:missing-associations c)))))

(deftest by-topic-filters
  (is (= ["ama.code-of-medical-ethics"]
         (mapv :association-rule/id (facts/by-topic "ama" :ethics))))
  (is (empty? (facts/by-topic "ama" :labor)))
  (is (empty? (facts/by-topic "wef" :governance))))
